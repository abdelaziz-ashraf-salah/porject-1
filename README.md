# library managment system

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












