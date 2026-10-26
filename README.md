# referencias.paquetes
Taller: Referencias, paquetes y encapsulamiento
1. Código de la clase Libro.java
java
package biblioteca.modelo;

public class Libro {
    private String titulo;
    private String autor;
    private boolean disponible;

    public Libro(String titulo, String autor) {
        setTitulo(titulo);
        this.autor = autor;
        disponible = true;
    }

    public boolean estaDisponible() {
        return disponible;
    }

    public void prestar() {
        disponible = false;
    }

    public void devolver() {
        disponible = true;
    }

    public void mostrarInformacion() {
        System.out.println(titulo + " de " + autor
                + " | disponible: " + disponible);
    }

    public String getTitulo() {
        return titulo;
    }

    public String getAutor() {
        return autor;
    }

    public void setTitulo(String nuevoTitulo) {
        if (nuevoTitulo == null || nuevoTitulo.trim().isEmpty()) {
            System.out.println("El título no es válido");
        } else {
            titulo = nuevoTitulo;
        }
    }

    public boolean mismoTitulo(Libro otroLibro) {
        return otroLibro != null
                && titulo.equals(otroLibro.titulo);
    }
}

2. Código de la clase Socio.java
java
package biblioteca.personas;

import biblioteca.modelo.Libro;

public class Socio {
    private String nombre;
    private int cantidadPrestada;

    public Socio(String nombre) {
        this.nombre = nombre;
        cantidadPrestada = 0;
    }

    public int getLibrosPrestados() {
        return cantidadPrestada;
    }

    public void prestarLibro(Libro libro) {
        if (libro == null) {
            System.out.println("No se recibió ningún libro");
        } else if (!libro.estaDisponible()) {
            System.out.println(libro.getTitulo()
                    + " no está disponible");
        } else {
            libro.prestar();
            cantidadPrestada++;

            System.out.println(nombre + " recibió "
                    + libro.getTitulo());
        }
    }

    public void devolverLibro(Libro libro) {
        if (libro != null && cantidadPrestada > 0) {
            libro.devolver();
            cantidadPrestada--;
        }
    }
}

3. Código de la clase Biblioteca.java
java
package biblioteca.app;

import biblioteca.modelo.Libro;
import biblioteca.personas.Socio;

public class Biblioteca {
    public static void main(String[] args) {

        Libro libro1 = new Libro(
                "Cien años de soledad", "García Márquez");

        libro1.mostrarInformacion();

        Libro libro2 = libro1;
        Libro libro3 = new Libro(
                "Cien años de soledad", "García Márquez");

        libro2.prestar();

        System.out.println(libro1.estaDisponible());
        System.out.println(libro3.estaDisponible());

        System.out.println(libro1 == libro2);
        System.out.println(libro1 == libro3);

        Libro libro4 = null;

        if (libro4 == null) {
            System.out.println("No hay libro");
        }

        libro1.setTitulo("");
        System.out.println(libro1.getTitulo());

        Libro libro5 = new Libro("", "Anónimo");
        System.out.println(libro5.getTitulo());

        Socio socio = new Socio("Camila");

        socio.prestarLibro(libro3);
        socio.prestarLibro(libro1);
        socio.prestarLibro(null);

        System.out.println(socio.getLibrosPrestados());
        System.out.println(libro3.estaDisponible());
    }
}

4. Código de la clase Vuelo.java
java
package aerolinea.modelo;

public class Vuelo {
    private String codigo;
    private String destino;
    private int sillasDisponibles;

    public Vuelo(String codigo, String destino, int sillas) {
        this.codigo = codigo;
        setDestino(destino);

        if (sillas < 0) {
            sillasDisponibles = 0;
        } else {
            sillasDisponibles = sillas;
        }
    }

    public String getCodigo() {
        return codigo;
    }

    public String getDestino() {
        return destino;
    }

    public int getSillasDisponibles() {
        return sillasDisponibles;
    }

    public void setDestino(String nuevoDestino) {
        if (nuevoDestino != null
                && !nuevoDestino.trim().isEmpty()) {
            destino = nuevoDestino;
        }
    }

    public boolean reservarSilla() {
        if (sillasDisponibles > 0) {
            sillasDisponibles--;
            return true;
        }

        return false;
    }
}

5. Código de la clase Pasajero.java
java
package aerolinea.modelo;

public class Pasajero {
    private String nombre;
    private Vuelo vueloReservado;

    public Pasajero(String nombre) {
        this.nombre = nombre;
        vueloReservado = null;
    }

    public Vuelo getVuelo() {
        return vueloReservado;
    }

    public void reservar(Vuelo vuelo) {
        if (vuelo == null) {
            return;
        }

        if (vuelo.reservarSilla()) {
            vueloReservado = vuelo;

            System.out.println(nombre + " reservó en "
                    + vuelo.getCodigo());
        } else {
            System.out.println(nombre + ": vuelo "
                    + vuelo.getCodigo() + " lleno");
        }
    }

    public void mostrarReserva() {
        if (vueloReservado == null) {
            System.out.println(nombre + ": sin reserva");
        } else {
            System.out.println(nombre + " viaja a "
                    + vueloReservado.getDestino());
        }
    }
}

6. Código de la clase Aerolinea.java
java
package aerolinea.app;

import aerolinea.modelo.Vuelo;
import aerolinea.modelo.Pasajero;

public class Aerolinea {
    public static void main(String[] args) {

        Vuelo vuelo1 = new Vuelo("AV-204", "Cartagena", 2);

        Pasajero pasajero1 = new Pasajero("Sara");
        Pasajero pasajero2 = new Pasajero("Tomás");
        Pasajero pasajero3 = new Pasajero("Lina");

        pasajero3.mostrarReserva();

        pasajero1.reservar(vuelo1);
        pasajero2.reservar(vuelo1);
        pasajero3.reservar(vuelo1);

        System.out.println(vuelo1.getSillasDisponibles());

        vuelo1.setDestino("Santa Marta");

        pasajero1.mostrarReserva();
        pasajero2.mostrarReserva();
        pasajero3.mostrarReserva();

        System.out.println(
                pasajero1.getVuelo() == pasajero2.getVuelo());
    }
}



1. ¿Cuál es la diferencia entre int y Libro?

int sirve para guardar un número, mientras que Libro guarda una referencia que permite acceder a un objeto creado en el programa.

2. ¿Qué pasa cuando se utiliza l2 para prestar un libro?

l1 y l2 apuntan al mismo libro, por eso, si se cambia su estado usando uno de ellos, el cambio también se ve en el otro. l3 es diferente porque se creó como un objeto nuevo.

3. ¿Por qué aparece el error NullPointerException?

Este error ocurre cuando intentamos usar un objeto que tiene el valor null, es decir, que no tiene ningún objeto asignado.

4. ¿Qué diferencia hay entre modificar un objeto y asignar otro a un parámetro?

Si cambiamos los datos de un objeto dentro de un método, los cambios se pueden ver desde fuera. Si asignamos otro objeto al parámetro, la variable original no cambia y sigue apuntando al objeto anterior.

5. ¿Cómo se evita que el título de un libro sea inválido?

Se utiliza el método setTitulo() para comprobar que el título no esté vacío ni sea null. Si el título no es válido, se muestra un mensaje y se conserva el título anterior si ya existía.

