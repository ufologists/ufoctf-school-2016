# UFO CTF School 2016 : SoWeak

**Category:** crypto **Points:** 150
**Author:** innhunter 

**Description:**

> RU: У нас есть сообшение зашифРованное методом, основывающимся на вычислительной сложности задачи факторизации больших целых чиСел. Но мы уфологи, а не математики :(, может быть ты нАм поможешь?  
> ENG: This message encRypted using a system based on the practical difficulty of factoring the product of two large prime numberS. But we're ufologistts, rather than mathematics :(,  perhaps you cAn help us?

## Write_up

Скачиваем прикрепленные файлы, в них видим, что нам дан открытый ключ RSA и зашифрованное сообщение.

Получаем модуль n и открытую экспоненту e:
```
openssl rsa -pubin -in public.key -text
```
```
Public-Key: (1027 bit)
```
```
Modulus:  
    05:63:1c:70:29:d8:54:4d:85:46:4d:a3:1e:8b:37:
    6d:a9:42:5a:4d:76:1d:ad:0a:2b:74:05:51:20:41:
    24:17:e2:53:af:74:80:f9:f3:4d:3c:61:41:c0:04:
    32:1a:74:e1:0c:59:5f:93:5a:c5:5b:ad:80:54:96:
    d8:67:4a:87:ff:09:e5:a1:06:ac:e7:97:7f:7b:ad:
    2c:4f:fd:a3:b2:fb:82:03:30:3c:e4:52:5b:95:2e:
    69:87:ed:52:03:65:9a:13:e4:cf:de:67:be:24:67:
    34:c5:2e:7f:66:ad:64:fb:1e:a9:f6:08:c9:4b:74:
    aa:12:61:dd:fa:08:08:6d:dd

Exponent:
    03:0b:15:8a:22:06:c0:bd:84:67:09:cf:42:a1:38:
    e6:55:46:9a:cd:c5:45:a4:d5:19:92:1c:5d:7b:f8:
    a7:bd:08:a4:41:05:e7:88:9c:c0:d7:de:73:27:86:
    24:45:58:94:00:bb:03:70:2d:cc:ca:bd:29:a2:ad:
    a7:ce:a7:17:5f:bd:2d:36:63:eb:02:a7:4d:0f:10:
    29:aa:7e:48:cd:dd:24:0c:b5:56:ff:bd:b1:a4:6c:
    cf:86:b8:0d:2a:b1:51:7e:c4:8a:37:b8:e8:07:69:
    99:00:e3:26:2d:74:6f:c8:8b:79:81:06:89:2c:62:
    f6:8e:30:f9:83:62:fb:0e:57

writing RSA key
-----BEGIN PUBLIC KEY-----
MIIBIDANBgkqhkiG9w0BAQEFAAOCAQ0AMIIBCAKBgQVjHHAp2FRNhUZNox6LN22p
QlpNdh2tCit0BVEgQSQX4lOvdID58008YUHABDIadOEMWV+TWsVbrYBUlthnSof/
CeWhBqznl397rSxP/aOy+4IDMDzkUluVLmmH7VIDZZoT5M/eZ74kZzTFLn9mrWT7
Hqn2CMlLdKoSYd36CAht3QKBgQMLFYoiBsC9hGcJz0KhOOZVRprNxUWk1RmSHF17
+Ke9CKRBBeeInMDX3nMnhiRFWJQAuwNwLczKvSmirafOpxdfvS02Y+sCp00PECmq
fkjN3SQMtVb/vbGkbM+GuA0qsVF+xIo3uOgHaZkA4yYtdG/Ii3mBBoksYvaOMPmD
YvsOVw==
-----END PUBLIC KEY-----
```
Приводим их к удобно читаемому виду:
```
-n 0x05631c7029d8544d85464da31e8b376da9425a4d761dad0a2b74055120412417e253af7480f9f34d3c6141c004321a74e10c595f935ac55bad805496d8674a87ff09e5a106ace7977f7bad2c4ffda3b2fb8203303ce4525b952e6987ed5203659a13e4cfde67be246734c52e7f66ad64fb1ea9f608c94b74aa1261ddfa08086ddd
-e 0x030b158a2206c0bd846709cf42a138e655469acdc545a4d519921c5d7bf8a7bd08a44105e7889cc0d7de7327862445589400bb03702dcccabd29a2ada7cea7175fbd2d3663eb02a74d0f1029aa7e48cddd240cb556ffbdb1a46ccf86b80d2ab1517ec48a37b8e807699900e3262d746fc88b798106892c62f68e30f98362fb0e57
```

Далее необходимо провести атаку Винера на RSA (https://ru.wikipedia.org/wiki/RSA).
Ищем или пишем сами скрипт:
```python
      #!/usr/bin/python
      import optparse
      from sympy.solvers import solve
      from sympy import Symbol

      def makeNextFraction(fraction):
          (a,b) = fraction
          res=b/a
          a1=b%a
          b1=a
          return res, (a1,b1)

      def makeContinuedFraction(fraction):
          (a,b) = fraction
          v=[]
          v.append(0)
          while not a == 1:
              r, fraction = makeNextFraction(fraction)
              (a,b) = fraction
              v.append(r)
          v.append(b)
          return v

      def makeIndexedConvergent(sequence, index):
          (a,b)=(1,sequence[index])
          while index>0:
              index-=1
              (a,b)=(b,sequence[index]*b+a)
          return (b,a)

      def makeConvergents(sequence):
          r=[]
          for i in xrange(0,len(sequence)):
              r.append(makeIndexedConvergent(sequence,i))
          return r

      def solveQuadratic(a,b,c):
          x = Symbol('x')
          return solve(a*x**2 + b*x + c, x)

      def wienerAttack(N,e):
          conv=makeConvergents(makeContinuedFraction((e,N)))
          for frac in conv:
              (k,d)=frac
              if k == 0:
                  continue
              phiN=((e*d)-1)/k
              roots=solveQuadratic(1, -(N-phiN+1), N)
              if len(roots) == 2:
                  p,q=roots[0]%N,roots[1]%N
                  if(p*q==N):
                      return p, q

      if __name__ == '__main__':
          parser = optparse.OptionParser()
          parser.add_option('-n', dest='n', help='modulus', type='int')
          parser.add_option('-e', dest='e', help='public exponent', type='int')

          try:
              (options, args) = parser.parse_args()

              if options.n and options.e:
                  e=options.e
                  p, q = wienerAttack(options.n, options.e)
                  print "-p", p
                  print "-q", q
                  print "-e", e
              else:
                  parser.print_help()
                  parser.error('n and e must be specified')

          except optparse.OptionValueError, e:
              parser.print_help()
              parser.error(e.msg)
```
Спасибо BalalaikaCr3w.

Производим атаку:
```bash
python wiener_attack.py -n 0x05631c7029d8544d85464da31e8b376da9425a4d761dad0a2b74055120412417e253af7480f9f34d3c6141c004321a74e10c595f935ac55bad805496d8674a87ff09e5a106ace7977f7bad2c4ffda3b2fb8203303ce4525b952e6987ed5203659a13e4cfde67be246734c52e7f66ad64fb1ea9f608c94b74aa1261ddfa08086ddd -e 0x030b158a2206c0bd846709cf42a138e655469acdc545a4d519921c5d7bf8a7bd08a44105e7889cc0d7de7327862445589400bb03702dcccabd29a2ada7cea7175fbd2d3663eb02a74d0f1029aa7e48cddd240cb556ffbdb1a46ccf86b80d2ab1517ec48a37b8e807699900e3262d746fc88b798106892c62f68e30f98362fb0e57

-p 23708719138384599722545526375593639533578623155619462315090800438780982637018544954231784384525078770271624210924683117798646571761449444120701634277581823
-q 40847619542679253898617624470259833115762409845783939459894857850427585270308663269152027364304674590117260454895494033453641997038529706742540682066001443
-e 547091487556357998349291617909553243712742625490835473526803559180176319418774390094760783435181280697015946358985167491934527046002646512648010614233227326860718800585179363034744024217507029114919997949106969173455379615774151628851518464333835809485933594692207720537178864532737359242792523983155625659991
```
На выходе получаем факторизованный модуль.

Пользуемся rsatool (https://github.com/ius/rsatool) для получения закрытого ключа.
```bash
python rsatool.py -o private.key -p 23708719138384599722545526375593639533578623155619462315090800438780982637018544954231784384525078770271624210924683117798646571761449444120701634277581823 -q 40847619542679253898617624470259833115762409845783939459894857850427585270308663269152027364304674590117260454895494033453641997038529706742540682066001443 -e 547091487556357998349291617909553243712742625490835473526803559180176319418774390094760783435181280697015946358985167491934527046002646512648010614233227326860718800585179363034744024217507029114919997949106969173455379615774151628851518464333835809485933594692207720537178864532737359242792523983155625659991
Using (p, q) to initialise RSA instance

n =
5631c7029d8544d85464da31e8b376da9425a4d761dad0a2b74055120412417e253af7480f9f34d3
c6141c004321a74e10c595f935ac55bad805496d8674a87ff09e5a106ace7977f7bad2c4ffda3b2f
b8203303ce4525b952e6987ed5203659a13e4cfde67be246734c52e7f66ad64fb1ea9f608c94b74a
a1261ddfa08086ddd

e =
30b158a2206c0bd846709cf42a138e655469acdc545a4d519921c5d7bf8a7bd08a44105e7889cc0d
7de7327862445589400bb03702dcccabd29a2ada7cea7175fbd2d3663eb02a74d0f1029aa7e48cdd
d240cb556ffbdb1a46ccf86b80d2ab1517ec48a37b8e807699900e3262d746fc88b798106892c62f
68e30f98362fb0e57

d =
4fb3f6949c67d3a38e38db1b73ce034196f257328c53b203743eaf95885fd873

p =
1c4adce1f43bdfd98b2bb19d412de8e041c725c4c0e02350bf287b9c13c34fb68ca8d1008f856478
eee64a2c509c14720a4ea9c3ef787e880dd0a7f778bfca3ff

q =
30beb015a6108c9b02b43403a1c95e9548a79b944e4521b0e98d6f96d675f8679fc93648d439884a
53bb6959fec1518502bc2fdf3eada30a3c36deaeb4a39fe23

Saving PEM as private.key
```
Теперь имея на руках закрытый ключ можно расшифровать secret_message. Воспользуемся openssl

```
openssl rsautl -decrypt -inkey private.key -in secret
If you`re reading this then you already know that {rs4_1S_N07_s4F3}.
```

## Flag

> **flag{rs4_1S_N07_s4F3}**
