# ATM
import java.util.Scanner;
class Menu{
    Scanner scan=new Scanner(System.in);
    float amount;
    public int enterPin(){
        System.out.println("Kindly enter the pin:");
        int pin=scan.nextInt();
        return pin;
    }

    public void exitOrStay(){
        System.out.println("Would you like to exit \n 1. Yes \n 2.No");
        int choosen=scan.nextInt();
        if(choosen==2) {
            selectMenu();
        }
        else exit();
    }

    public void selectMenu(){
        System.out.println("Select option from the menu:\n 1: A/C Balance      2. Withdraw money \n 3. Deposit money    4. Exit");
        int choosen=scan.nextInt();
        switch(choosen){
            case 1:checkBalance();
                break;
            case 2:withdrawMoney();
                break;
            case 3:depositMoney();
                break;
            case 4:exit();
        }
    }

    public void checkBalance(){
        System.out.println("The balance in your account is "+amount);
        exitOrStay();
    }

    public void withdrawMoney(){
        System.out.println("Please enter the amount to be withdrawn");
        int withdraw=scan.nextInt();
        if(withdraw<amount) {
            System.out.println("The " + withdraw + "  is withdrawn from the account.");
            amount=amount-withdraw;
            System.out.println("Updated balance is "+amount);
        }
        else if(amount>0)
        {
            System.out.println("Insufficient balance. Kindly withdraw less "+amount);
        }
        else
            System.out.println("The balance is 0 or less, money cannot be withdrawn");

        exitOrStay();
    }

    public void depositMoney(){
        System.out.println("Please enter the amount to be deposited");
        int deposit=scan.nextInt();
        System.out.println("The "+deposit+"  is deposited into the account.");
        amount=amount+deposit;
        System.out.println("Updated balance is "+amount);
        exitOrStay();
    }

    public void exit(){
        System.out.println("Thanks for using the service");
    }
}
public class Main {
    public static void main(String[] args) throws InterruptedException {

        System.out.println("Welcome to the ATM");

        Thread.sleep(1000);

        Menu menu=new Menu();
        int chance=3;
        boolean flag=false;
        while(chance>0){
            int pin=menu.enterPin();
            if (pin==123){
                chance=0;
                flag=true;
                menu.selectMenu();
            }
            else{
                chance--;
                    System.out.println("The entered pin is incorrect. You have "+chance+" more chances");
            }
        }
        if(flag==false) {
            System.out.println("Attempt exhausted. Card is blocked. Kindly re-attempt after 45 minutes");
        }
    }
}
