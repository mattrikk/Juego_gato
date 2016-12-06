# Juego_gato
package recursividad;


import java.util.Scanner;
public class PilayCola
{
    private String[]    jugadores   = new String[2];
    private String[][]  juego       = new String[3][3];
    private Scanner     scan        = new Scanner(System.in);
    private boolean     jugando     = true,yaIngresado=false;
    private int         jugadorsh   = 1,turnos=0;
    public PilayCola()
    {
        jugadores[0]="X";
        jugadores[1]="O";
        llenaArreglo();
        do {
            System.out.println("Turno Jugador ["+jugadorsh+"]");
            while(!yaIngresado) {
                imprimeGato();
                System.out.println("Ingresa Fila:");
                int px=Integer.parseInt(scan.nextLine());
                System.out.println("Ingresa Columna:");
                int py=Integer.parseInt(scan.nextLine());
                yaIngresado = agregaPosicion(px-1,py-1,jugadores[jugadorsh-1]);
                if (!yaIngresado) System.out.println("ERROR: Casilla ya ingresada o Fuera del Rango");
            }
            if (compruebaGana()) {
                imprimeGato();
                System.out.println("Jugador ["+jugadorsh+"] ha ganado "+jugadores[jugadorsh-1]);
                return;
            }
            if (turnos==8) System.out.println("Emplate!");
            jugadorsh++;
            if (jugadorsh == 3) jugadorsh = 1;
            yaIngresado=false;
        } while(jugando);
    }
    public boolean agregaPosicion(int x, int y,String val){
        try {
            if (juego[x][y]==" ") {
                juego[x][y] = val;
                turnos++;
                return true;
            }
        } catch(Exception e) { return false; }
        return false;
    }
    public void llenaArreglo(){
        for(int i=0; i <3; i++) { for(int j=0; j <3; j++) { juego[i][j]=  " "; } }
    }
    public void imprimeGato() {
        System.out.println("    1  2  3");
        for(int i=0; i <3; i++) {
            for(int j=0; j <3; j++) {
                if (j==0) System.out.print(i+1);
                System.out.print(" |"+juego[i][j]);
            }
            System.out.println(" |");
        }
    }
    public boolean compruebaGana() {
        for(int i=0; i <3; i++) {
            if (juego[0][0] == juego[1][1] && juego[1][1] == juego[2][2] && juego[1][1] != " ") return true;
            else if (juego[0][2] == juego[1][1] && juego[1][1] == juego[2][0] && juego[1][1] != " ") return true;
            else if (juego[i][0] == juego[i][1] && juego[i][1] == juego[i][2] && juego[i][1] != " ") return true;
            else if (juego[0][i] == juego[1][i] && juego[1][i] == juego[2][i] && juego[1][i] != " ") return true;
            else{
                System.out.println("El Juego a terminado nadie Gano!!");
            
        }
        }
        return false;
        
        
        
        
    }
    
    
    
    
    
    
    public static void main(String[] args) {
        PilayCola tc=new PilayCola();
        
        tc.compruebaGana();
        tc.imprimeGato();
        
    }
}
