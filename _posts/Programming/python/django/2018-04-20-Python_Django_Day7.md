---
key: 20180413
title: Python & Django Day7 Class
tags: [django, python]
categories: programming
comments: true
---

  Fastcampus Python&Django 온라인 강의를 듣고 작성한 Class note입니다.

<br>

# Class

```python
def print_hello(name):
	print("Hello ", name)

# 함수는 다른 변수명에도 저장할 수 있음
print_hello_name = print_hello
print_hello_name("Jane")

# 함수는 list에도 넣을 수 있음
func_list = [print_hello, 1, 2]
func_list[0]('Jane')

# 함수는 dictionary에도 넣을 수 있음
func_dict = {
	'func': print_hello
}

func_dict['func']('Jane')

```

<br>

```python
MY_MONEY = [0]

def spend(m):
	if MY_MONEY[0] > m:
		MY_MONEY[0] -= m
		print("{}를 사용했습니다. 남은 잔액 : {}".format(m, MY_MONEY[0]))
	else:
		print("가지고 있는 돈이 부족합니다.")

def income(m):
	MY_MONEY[0] += m
	print("{}를 벌었습니다. 남은 잔액 : {}".format(m, MY_MONEY[0]))

wallet = {
	'money': MY_MONEY,
	'spend': spend
}



>>> from file import wallet
>>> wallet['income'](10000)
10000를 벌었습니다. 남은 잔액 : 10000
>>> wallet['spend'](5000)
5000를 사용했습니다. 남은 잔액 : 5000

```

내 지갑 외에 다른 사람 지갑 만들기 위해서는 위 작업을 동일하게 거쳐야 하기 때문에 매우 힘들다. 그래서 class를 만들어 두면 복제가 빠르다.

<br><br>



### class Wallet: pass

```python
class Wallet(object): # (object) 생략가능. 자동상속 받음.
	pass

my_wallet = Wallet()

print(my_wallet)
```

<br>

#### 처음 객체가 생성될 때 실행되는 메소드 :     __init__ 

**def ______init__(self):**

```python
class Wallet: 
	def __init__(self, name):
		self.owner = name
	
	def print_owner_name(self):
		print(self.owner)

my_wallet = Wallet('sol')

print(my_wallet.owner)
```

클래스가 객체를 만들 때, 객체 자기자신을 의미 하는 것이 self.

 <br>

####  지갑 만들기

```python
class Wallet: 
	money = 0

	def __init__(self, name):
        print("{}님 환영합니다.".format(name))
		self.owner = name
	
	def print_owner_name(self):
		print('owner name is ', self.owner)

	def print_now_money(self):
		print("현재 잔액은 : ", self.money)

	def spend(self, m):
		if self.money < m:
			print("돈이 부족합니다.")
			self.print_now_money()
		else:
			self.money -= m
			print("{}를 지출했습니다.".format(m))
			self.print_now_money()
	def income(self, m):
		self.money += m
		print("{}를 입금했습니다.".format(m))
		self.print_now_money()
	
	
----------------------------------------------------

>>> from file import Wallet
>>> sol_wallet = Wallet('sol')
>>> sol_wallet.owner
'sol'
>>> sol_wallet.spend(100)
돈이 부족합니다.
현재 잔액은 0
>>> sol_wallet.income(10000)
10000을 입금했습니다.
현재 잔액은 10000

```



<br><br>

## Class (2)

### 상속

```python
# 부모 클래스의 메소드와 변수들을 가져온다

class Child(Parent):
	pass
```

<br>

```python
class ChildWallet(Wallet):
    pass
```

 python의 모든 클래스는 자동적으로 object를 상속 받는다. `issubclass(ChildWallet, Wallet)` 를 통해서 상속받았는지 확인 가능하다. (True, False 반환해 줌)

<br>

```python
class Account(Wallet):
    def send_money(self, money, to):
        if self.money > money:
            to.money += money
            self.money -= money
            print("{}원을 {}에게 보냈습니다.".format(money, to.owner))
            self.print_now_money()

-----------------------------------------------------------------

>>> forme file import Account
>>> sol_a = Account('sol')
>>> sol_a.income(1000000)
>>> sol_a.money
>>> suzy_a = Account('suzy')
>>> sol_a.send_money(100000, suzy_a)
```

<br>



### 오버라이드

```python
class Child(Parent):
    pass
```

<br>

```python
class Account(Wallet):
    def __init__(self, name, account_number):
        self.account_number = account_number
        super().__init__(name)	# 부모 클래스에서 호출
    
    def __str__(self):
        return '{}의 계좌입니다. 계좌번호 :'.format(self.owner, self.account_number)
    
    def __repr__(self):
        return '{}의 계좌입니다. 계좌번호 :'.format(self.owner, self.account_number)
    
    def __add__(self, another):
        return self.money + another.money
    
    def __call__(self):
        print("호출되었습니다.")
    
    def send_money(self, money, to):
        if self.money > money:
            to.money += money
            self.money -= money
            print("{}원을 {}에게 보냈습니다.".format(money, to.owner))
            self.print_now_money()

----------------------------------------------------
>>> from file import Account
>>> sol_a = Account('sol', '123-123456')
>>> sol_a.account_number
>>> 
```

<br>

### super() 

부모 호출

<br>

### Python Special Method

#### ______str__()

#### ______call__()

#### ______add()__(y)



```python
class Wallet: 
	money = 0

	def __init__(self, name):
        print("{}님 환영합니다.".format(name))
		self.owner = name

    #-------------- Special Method --------------#
    def __str__(self):
        return '{}의 지갑입니다.'.format(self.owner)
    
    def __repr__(self):
        return '{}의 지갑입니다.'.format(self.owner)
	#--------------------------------------------#
    
    
	def print_owner_name(self):
		print('owner name is ', self.owner)

	def print_now_money(self):
		print("현재 잔액은 : ", self.money)

	def spend(self, m):
		if self.money < m:
			print("돈이 부족합니다.")
			self.print_now_money()
		else:
			self.money -= m
			print("{}를 지출했습니다ㅇ.".format(m))
			self.print_now_money()
	def income(self, m):
		self.money += m
		print("{}를 입금했습니다.".format(m))
		self.print_now_money()
```

