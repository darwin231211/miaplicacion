import java.io.*;
import java.util.*;

public class MiAplicacion {
    private final List<String> listaDatos; // Ejemplo de List
    private final Map<Integer, String> mapaDatos; // Ejemplo de Map

    public MiAplicacion() {
        listaDatos = new ArrayList<>();
        mapaDatos = new HashMap<>();
    }

    // Métodos para List
    public void agregarElementoLista(String elemento) {
        listaDatos.add(elemento);
    }

    public void eliminarElementoLista(String elemento) {
        if (listaDatos.remove(elemento)) {
            System.out.println("Elemento eliminado de la lista.");
        } else {
            System.out.println("Elemento no encontrado en la lista.");
        }
    }

    public void modificarElementoLista(String elementoOriginal, String nuevoElemento) {
        int index = listaDatos.indexOf(elementoOriginal);
        if (index != -1) {
            listaDatos.set(index, nuevoElemento);
            System.out.println("Elemento modificado.");
        } else {
            System.out.println("Elemento no encontrado.");
        }
    }

    public void buscarElementoLista(String elemento) {
        if (listaDatos.contains(elemento)) {
            System.out.println("Elemento encontrado en la lista.");
        } else {
            System.out.println("Elemento no encontrado en la lista.");
        }
    }

    public void mostrarLista() {
        System.out.println("Contenido de la lista: " + listaDatos);
    }

    // Métodos para Map
    public void agregarElementoMapa(int clave, String valor) {
        mapaDatos.put(clave, valor);
    }

    public void eliminarElementoMapa(int clave) {
        if (mapaDatos.remove(clave) != null) {
            System.out.println("Elemento eliminado del mapa.");
        } else {
            System.out.println("Clave no encontrada en el mapa.");
        }
    }

    public void modificarElementoMapa(int clave, String nuevoValor) {
        if (mapaDatos.containsKey(clave)) {
            mapaDatos.put(clave, nuevoValor);
            System.out.println("Elemento modificado.");
        } else {
            System.out.println("Clave no encontrada en el mapa.");
        }
    }

    public void buscarElementoMapa(int clave) {
        if (mapaDatos.containsKey(clave)) {
            System.out.println("Valor asociado a la clave " + clave + ": " + mapaDatos.get(clave));
        } else {
            System.out.println("Clave no encontrada en el mapa.");
        }
    }

    public void mostrarMapa() {
        System.out.println("Contenido del mapa: " + mapaDatos);
    }

    // Manipulación de archivos
    public void guardarDatosEnArchivo(String nombreArchivo) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(nombreArchivo))) {
            writer.write("Lista:\n");
            for (String elemento : listaDatos) {
                writer.write(elemento + "\n");
            }
            writer.write("Mapa:\n");
            for (Map.Entry<Integer, String> entrada : mapaDatos.entrySet()) {
                writer.write(entrada.getKey() + ":" + entrada.getValue() + "\n");
            }
            System.out.println("Datos guardados en el archivo.");
        } catch (IOException e) {
            System.out.println("Error al guardar los datos: " + e.getMessage());
        }
    }

    public void cargarDatosDesdeArchivo(String nombreArchivo) {
        try (BufferedReader reader = new BufferedReader(new FileReader(nombreArchivo))) {
            String linea;
            boolean esLista = true;
            while ((linea = reader.readLine()) != null) {
                if (linea.equals("Mapa:")) {
                    esLista = false;
                } else if (!linea.equals("Lista:")) {
                    if (esLista) {
                        listaDatos.add(linea);
                    } else {
                        String[] partes = linea.split(":");
                        mapaDatos.put(Integer.valueOf(partes[0]), partes[1]);
                    }
                }
            }
            System.out.println("Datos cargados desde el archivo.");
        } catch (IOException e) {
            System.out.println("Error al cargar los datos: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        MiAplicacion app = new MiAplicacion();

        // Operaciones de prueba
        app.agregarElementoLista("Elemento1");
        app.modificarElementoLista("Elemento1", "NuevoElemento1");
        app.buscarElementoLista("NuevoElemento1");
        app.mostrarLista();
        app.guardarDatosEnArchivo("datos.txt");
        app.cargarDatosDesdeArchivo("datos.txt");

        app.agregarElementoMapa(1, "Valor1");
        app.modificarElementoMapa(1, "NuevoValor1");
        app.buscarElementoMapa(1);
        app.mostrarMapa();
        app.guardarDatosEnArchivo("datos.txt");
        app.cargarDatosDesdeArchivo("datos.txt");
    }
}
