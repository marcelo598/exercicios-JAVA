# exercicios-JAVA
public class ContaBanco {
    public int numConta;
    protected String tipo;
    private String dono;
    private float saldo;
    private boolean status;

    public void estadoAtual(){
        System.out.println("conta: " + this.getNumConta());
        System.out.println("tipo: " + this.getTipo());
        System.out.println("dono: " + this.getDono());
        System.out.println("saldo: " + this.getSaldo());
        System.out.println("status: " + this.getStatus());
    }

    public void abrirConta(String tipo){
        this.settipo(tipo);
        this.setstatus(true);
        if ( tipo == "CC") {
            this.setSaldo(50);
        }else if (tipo == "CP"){
            this.saldo = 150;
        }
        System.out.println("Conta aberta com sucesso");
    }
    public void fecharConta(){
        if (this.getSaldo()>0){
            System.out.println("Conta nao pode ser fechada pq ainda tem dinheiro");
        }else if(this.getSaldo()<0){
            System.out.println("Conta nao pode ser fechada pois ainda tem débito");
        }else{
            this.setstatus(false);
            System.out.println("conta fechado com sucesso");
        }
    }
    public void depositar(float v){
       if( this.getStatus()){
           //this.saldo = this.saldo + v;
           this.setSaldo(this.getSaldo() + v);
           System.out.println("deposito realizado na conta de " + this.getDono());
    } else {
          System.out.println("impossivel depositar em uma conta fechada ");
       }
    }
    public void sacar(float v){
        if (this.getStatus()) {
            if (this.getSaldo() >= v) {
                this.setSaldo(this.getSaldo() - v);
                System.out.println("Saque realizado na conta de " + this.getDono());
            } else {
                System.out.println("Saldo insuficiente para saque");
            }
        } else {
            System.out.println("Impossível sacar de uma conta fechada");
        }
    }

    public void pagarMensal() {
        int v = 0;

        if (this.getTipo() == "CC") {
            v = 12;
        } else if (this.getTipo() == "CP") {
            v = 20;
        }

        if (this.getStatus()) {
            this.setSaldo(this.getSaldo() - v);
            System.out.println("Mensalidade paga com sucesso por " + this.getDono());
        } else {
            System.out.println("Impossível pagar uma conta fechada!");
        }
    }

    public ContaBanco(){
        this.saldo =0;
        this.status=false;
    }
    public void setNumConta( int n){
        this.numConta = n;
    }
    public int getNumConta(){
        return this.numConta;
    }
    public String setDono( String dono){
        return this.dono= dono;
    }
    public String getDono() {
        return this.dono;
    }
    public float getSaldo(){
        return this.saldo;
    }
    public void setSaldo(float saldo){
        this.saldo=saldo;
    }
    public boolean getStatus(){
        return this.status;
    }
    public void setstatus(boolean status){
        this.status=status;
    }
    public String settipo( String tipo){
        return this.tipo= tipo;
    }
    public String getTipo() {
        return this.tipo;

}}

public class Main {
    public static void main(String[] args){
        ContaBanco b1 = new ContaBanco();
        b1.setNumConta(1111);
        b1.setDono("Augusto");
        b1.abrirConta("CC");

        ContaBanco b2 = new ContaBanco();
        b2.setNumConta(2222);
        b2.setDono("Creuza");
        b2.abrirConta("CP");

        b1.depositar(100);
        b2.depositar(500);
        b2.sacar(100);

        b1.estadoAtual();
        b2.estadoAtual();
    }
}



