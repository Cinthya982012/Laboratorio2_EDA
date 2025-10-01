import java.util.*;
import java.util.Random;
import java.util.Locale;
import java.util.Stack;

/**
 LABORATORIO 2: PILAS Y COLAS
 UNIVERSIDAD DIEGO PORTALES
 PROFESOR: CRISTIÁN LLULL
 INTEGRANTES:
 -CINTHYA FUENTEALBA BRAVO
 -IGNACIA REYES OJEDA
 */
//================================================================================
//CLASE NODO
class Nodo<T>{
    private T valor;
    private Nodo<T> siguiente;

    /**Constructor vacio*/
    public Nodo(){
        valor = null;
        siguiente = null;
    }

    /**Constructor con valor*/
    public Nodo(T valor){
        this.valor = valor;
        this.siguiente = null;
    }

    /**Constructor con valor y siguiente*/
    public Nodo(T valor, Nodo<T> siguiente){
        this.valor = valor;
        this.siguiente = siguiente;
    }

    //SETTERS Y GETTERS
    public T getValor(){return valor;}
    public Nodo<T> getSiguiente(){return siguiente;}

    public void setValor(T valor){this.valor = valor;}
    public void setSiguiente(Nodo<T> siguiente){this.siguiente = siguiente;}
}

//================================================================================
//CLASE PILA ENLAZADA
class PilaEnlazada<T>{
    Stack<T>pila=new Stack<>();

    //ATRIBUTOS CLASE PILA ENLAZADA
    private Nodo<T>tope;
    private int size;

    //MÉTODOS CLASE PILA ENLAZADA
    /**Push*/
    public void push(T valor){
        Nodo<T>nuevo = new Nodo<>(valor, tope);
        tope = nuevo;
        size++;
    }

    /**Pop*/
    public T pop(){
        if(isEmpty()==true){return null;}

        T valor = tope.getValor();
        tope = tope.getSiguiente();
        size--;
        return valor;
    }
    /**Peek*/
    public T peek(){
        if(isEmpty()==true){return null;}
        return tope.getValor();
    }
    /**Boolean*/
    public boolean isEmpty(){return tope == null;}

    /**String to String(Imprimir pila)*/
    public String toString(){
        String string =" ";
        Nodo<T>actual = tope; //Comienza desde el inicio
        while(actual!=null){ //Recorre la pila hasta el final
            string += actual.getSiguiente(); //Suma el valor + un espacio
            actual = actual.getSiguiente();//Devuelve el string
        }
        return string;
    }
    public int size(){return size;}
    public void vaciar(){
        while(!pila.isEmpty()){pila.pop();}
    }
}
//================================================================================
//CLASE COLA ENLAZADA
class ColaEnlazada<T>{
    //ATRIBUTOS CLASE COLA ENLAZADA
    private Nodo<T>inicio;
    private Nodo<T>fin;
    private int size;

    //MÉTODOS CLASE COLA ENLAZADA
    /**Boolean*/
    public boolean add(T valor){
        Nodo<T>nuevo = new Nodo<>(valor);//Creación de un nodo nuevo

        if(inicio==null){//Si la cola esta vacia
            inicio = nuevo;
            fin = nuevo;
        }
        else{//Si ya existen elementos
            fin.setSiguiente(nuevo);//El ultimo nodo apunta al nuevo
            fin = nuevo;
        }
        size++;//Aumentar el tamaño
        return true;//Devolver true (Proceso exitoso)
    }

    /**Pool*/
    public T poll(){
        if(inicio==null){return null;}//Si la cola esta vacia. No hay nodo inicial, no hay nada por quitar.
        T valor = inicio.getValor();//Guarda el valor del nodo inicial
        inicio = inicio.getSiguiente();//Avanza el puntero de inicio al siguiente nodo
        size--;//Disminuye el tamaño de la cola
        return valor;//Retorna el valor que se quito
    }

    /**Peek*/
    public T peek(){
        if(inicio==null){return null;}//Si la cola esta vacia retotna null
        return inicio.getValor();//Si existe algo en la cola devuelve el valor del primer nodo.
    }

    /**Boolean is Empty*/
    public boolean isEmpty(){
        if(inicio==null){return true;}//Si la cola esta vacia retorna true
        else{return false;}//Si la cola no esta vacia retorna false
    }
}
//================================================================================
//CLASE ALERTA
class Alerta{
    //ATRIBUTOS CLASE ALERTA
    private String nombre;
    private double probFallo;// Probabilidad de fallo entre 0 y 1
    private int limiteAlertas;
    private Random rng;//Numeros al azar entre 0 y 1

    public String getNombre(){return nombre;}

    //METODOS CLASE ALERTA
    /**Constructor 1*/
    public Alerta(String nombre, double probFallo){
        this.nombre = nombre;
        this.probFallo = probFallo;
    }

    /**Constructor 2*/
    public Alerta(String nombre, double probFallo, Random rng){
        this.nombre = nombre;
        this.probFallo = probFallo;
        this.rng = rng;//Guarda el numero al azar que se da
    }


    public boolean procesarLlamada(PilaEnlazada<Alerta>pila, int limite){
        /**Caso Base (Alcanzar la profundidad maxima)*/
        if(pila.size()>=limite){return true;}//Si el tamaño de la pila llego al limite, ya se alcanzo la profundidad maxima y retorna true

        /**Caso 1: Posible falla aleatoria*/
        double fallo=rng.nextDouble();//Se genera un número aleatorio entre 0 y 1
        if(fallo <this.probFallo){return false;}//Si el fallo es menor que la probabilidad de fallo. La alerta falla y retorna false.

        /**Caso 2: Recursivo (generar la siguiente alerta y continuar)*/
        String idNueva = "Alerta Nivel" + pila.size();//Nombre para la nueva alerta
        Alerta siguiente = new Alerta(idNueva, probFallo, rng); //Se crea una nueva alerta con el mismo numero al azar
        pila.push(siguiente);//Se mete a la pila en la parte top
        return siguiente.procesarLlamada(pila, limite);//Se llama recursivamente el metodo procesarLlamado
    }

    public String mostrarAlerta(){
        return nombre + "(Alerta Prob. Fallo= " + probFallo + ")";
    }
}
//================================================================================
//CLASE MAIN
public class Main {
    //ATRIBUTOS CLASE MAINRNG para Reproducibilidad
    static long semilla=42L;//Semilla
    static double probfallo=0.10;//Probabilidad de fallo
    static int numAlertas=5;//Numero de alertas que se tienen
    static int limiteRecursion=10;//Limite de hasta donde se puede llegar

    //METODOS CLASE MAIN
    public static void generarAlerta(int numeAlertas){}
    public static void iniciarSimulacion(){}

    public static void main(String[] args) {//Lectura de los parametros por linea
        if(args.length>=1){semilla=Long.parseLong(args[0]);}//Semilla
        if(args.length>=2){probfallo=Double.parseDouble(args[1]);}//Probabilidad de fallo
        if(args.length>=3){numAlertas=Integer.parseInt(args[2]);}//Numero de alertas
        if(args.length>=4){limiteRecursion=Integer.parseInt(args[3]);}//Limite recursion

        Random rng=new Random(semilla);//RNG se encuentra inicializado con semilla

        /**Estructuras de datos principales*/
        ColaEnlazada<Alerta>cola=new ColaEnlazada<>();//Cola (FIFO)
        PilaEnlazada<Alerta>pila=new PilaEnlazada<>();//Pila (LIFO)

        for(int i=0; i < numAlertas; i++){//Genera numero de alertas con misma probabilidad
            cola.add(new Alerta("Alerta"+i, probfallo, rng));//Las añade a una cola (misma probabilidad)
        }

        /**Contadores*/
        int exitos=0;//Numero de alertas que son exitosas
        int fallo=0;//Numero de alertas que fallan
        long tiempo=System.nanoTime();//Mide la duracion total

        /**La cola no esta vacia(la va vaciando)*/
        while(!cola.isEmpty()){
            Alerta a1 = cola.poll();//Toma la siguiente alerta (FIFO)
            System.out.println(">> Procesando a " + a1.getNombre());
            pila.push(a1);//Empuja la alerta a la pila de llamadas

            /**Se ejecuta un flujo recursivo de alerta , hasta encontrar la profundidad máxima*/
            boolean ok= a1.procesarLlamada(pila, limiteRecursion);
            if(ok){//Indica exito
                exitos++;
                System.out.println(">> Exito: Alcanzo el límite" + limiteRecursion);
            }
            else{//Indica fallo
                fallo++;
                System.out.println(">> Fallo: Se interrumpio");
                System.out.println("Pofundidad: " + pila.size());
            }

            pila.vaciar();//Limpia la pila antes de ir a la siguiente alerta
            System.out.println("-----");
        }
        /**Tiempo total de la simulación en milisegundos*/
        long dt = System.nanoTime()-tiempo;
        System.out.printf(Locale.US, "Resumen -> exitos=%d, fallos=%d, tiempoMs=%.3f%n", exitos, fallo, dt/1e6);
    }
}
