# library managment system and bank system

class library:
    def _init_(self,email,password,ownermail,ownerpass,fullname,SSN):
        self.email = email
        self.password = password
        self.fullname = fullname
        self.SSN = SSN
        self.ownermail = ownermail
        self.ownerpass = ownerpass
       

        
    def open_account(self):
        fullname = str(input('please enter your full name'))
        SSN = int(input('please enter your national number'))
        email = str(input('please enter your email'))
        password = int(input('please enter your bassword ,just numbers'))
        address = str(input('please enter your address'))
        phone = int(input('please enter your phone number'))        
        
        
        
        
    def adminstrator(self,email,owneremail,password):
        if self.ownermail == email and self.ownerpass == password:    
            return ('you are logged as a librarian')
        else:
            return ('the email is wrong')
        
    def login(self,email,password):
        if self.email == email and self.password == password:
            return ('you are logged in as a user')
        else:
            return ('there is wrong in email or password')
        
class userAccount(library):
    def _init_(self,email,password,fullname,phone,SSN,address):
        super()._init_(email, password, fullname, phone, SSN, address)
        self.account_type = 'user account' 
        
        
class ownermail(library):
    def _init_(self, email, password, ownermail, ownerpass, fullname, SSN):
        super()._init_(email, password, ownermail, ownerpass, fullname, SSN)
        self.account_type = 'owner account'
    
        
        
def login(accounts,password,email):
    for account in accounts:
        if account.login(email,password):
               return account
    return
def main():
    accounts = []
    print('Welcom To library')
    while True :
        choice = None
        account = None
        print('To create Account Press 1')
        print('To login as user Account Press 2')
        print('To login as authentication Account Press 3')
        choice = input()
        if choice =='1':
            print('To create user Account Press 1')
            choice = input()
            fullname = input('Enter Name :')
            email = input('Enter email :')
            SSN = input('Enter SSN :')
            address = input('Enter address :')
            phone = input('Enter phone :')
            password = input('Enter Password :')
            if choice =='1':
                account = userAccount(email, password, fullname, phone, SSN, address)
            accounts.append(account)
            print('your account has been created ')
            continue
        if choice =='2':
            email = input('enter email :')
            password = input('enter password :')
            account = login(accounts,password,email)
            if account == None :
                
                print('can not find your account')
            else:
                    print('you are logged in ')                 
                    continue
        if choice == '3':
           email = input('enter email :')
           password = input('enter password :')
           account = login(accounts,password,email)
           if account == None :
               
               print('can not find your account')
           else:
                   print('you are logged in ')                 
                   continue
            
         
main()




#managment bank system account

class Account:
    def __init__(self,email,password,name,phone,ssn,address):
        # check for user 
        self._ssn = ssn
        self.email = email
        self.name = name
        self.phone = phone
        self.address = address
        self.__is_authenticated = False
        self.set_password(password)
        self.open_account()
        
    def set_password(self,password):
        self.__password = password
    
    def reset_password(self,old_password,password):
        if not self.check_password(old_password):
            print('your old password is not correct')
        self.__password = password
    
    def open_account(self):
        self.account_no = self._ssn
        self.balance = 0
    
    def check_password(self,password):
        if password != self.__password:
            return False
        return True
    def authentication(self,email,password):
        if email != self.email:
            return False 
        return self.check_password(password)
    
    
    def login(self,email,password):
        self.__is_authenticated = self.authentication(email,password)
    
    def logout(self):
        self.__is_authenticated = False
    
    def _is_authenecated(self):
        return self.__is_authenticated       
    
    def withdroaw(self,amount):
        if not self.is_authenecated():
            print('user are not authorized')
            return
        if amount > self.check_balance():
            print('there is no enough balance in your account')
            return 
        self.balance -= amount
        
    def deposit(self,amount):
        if not self.is_authenecated():
            print('user are not authorized')
            return
        self.balance += amount
    
    def check_balance(self):
        if not self.is_authenecated():
            print('user are not authorized')
            return
        return self.balance
    
    def print_info(self):
        if not self.is_authenecated():
            print('user are not authorized')
        print(f'name = {self.name}  \
              , balance = {self.balance} , phone = {self.phone} , \
                  address = {self.address}')
    
    
    
class SavingAccount(Account):
    def __init__(self,email,password,name,phone,ssn,address):
        super().__init__(email, password, name, phone, ssn, address)
        self.account_type = 'SA'
    
    
    def deposit(self,amount):
        if not self.is_authenecated():
            print('user are not authorized')
            return
        profit = amount * 0.18
        self.balance += amount
        self.balance += profit

class CurrentAccount(Account):
    def __init__(self,email,password,name,phone,ssn,address):
        super().__init__(email, password, name, phone, ssn, address)
        self.account_type = 'CA'


def login(accounts,password,email):
    for account in accounts:
        if account.login(email,password):
               return account
    return

def main():
    accounts = []
    print('Welcom To Banck')
    while True :
        choice = None
        account = None
        print('To create Account Press 1')
        print('To Login Press 2')
        choice = input()
        if choice =='1':
            print('To create Current Account Press 1')
            print('To create Saving Account Press 2')
            choice = input()
            name = input('Enter Name')
            email = input('Enter email')
            ssn = input('Enter SSN')
            address = input('Enter address')
            phone = input('Enter phone')
            password = input('Enter Password')
            if choice =='1':
                account = CurrentAccount(email, password, name, phone, ssn, address)
            if choice =='2':
                account = SavingAccount(email, password, name, phone, ssn, address)
            accounts.append(account)
            print('your account has been created ')
            continue
        if choice == '2':
            email = input('enter email')
            password = input('enter password')
            account = login(accounts,password,email)
            if account == None :
                print('can not find your account')
                continue
            print(account.check_balance())
            
main()







