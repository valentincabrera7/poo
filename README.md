# poo (se llama la carpeta)

# abstraccion.py
# CLASES ABSTRACTAS:

from abc import ABC, abstractmethod 
                     # DECORADOR

class Persona(ABC): # ya con ABC se crea una clase abstracta

    @abstractmethod # con este decorador ya estamos diciendo que vamos a crear un metodo abstracto

    def __init__(self, nombre, edad, sexo, actividad):
        self.nombre = nombre
        self.edad = edad 
        self.sexo = sexo
        self.actividad = actividad

    @abstractmethod

    def hacer_actividad(self):
        pass

    def presentarse(self): # esto no es una clase abstracta
        print(f"Hola me llamo {self.nombre} y tengo {self.edad} años.")

class Estudiante(Persona):

    def __init__(self, nombre, edad, sexo, actividad):
        super().__init__(nombre, edad, sexo, actividad)
    
    def hacer_actividad(self):
        print(f"Estoy estudiando {self.actividad}")

class Trabajador(Persona):

    def __init__(self, nombre, edad, sexo, actividad):
        super().__init__(nombre, edad, sexo, actividad)
    
    def hacer_actividad(self):
        print(f"Estoy trabajando como {self.actividad}")


valentin = Estudiante("Valentin", 25, "Masculino", "Programación")
valentin1 = Trabajador("Valentin", 25, "Masculino", "Programador")

print(valentin.nombre) # para acceder a los atributos de self
print(valentin.edad)
print(valentin.sexo)
valentin.hacer_actividad() # para acceder a los metodos(funciones)

print(valentin1.nombre)
print(valentin1.edad)
print(valentin1.sexo)
valentin1.hacer_actividad()

# clase, obj, metodos.py

class Celular(): # esto es una clase
    def __init__(self, marca, modelo, camara): # metodo constructor de objetos
        self.marca = marca
        self.modelo = modelo  # self es como decir, celular.marca/modelo/camara
        self.camara = camara

    def llamar(self): # metodo
        print(f"Realizando un llamada desde: {self.marca} {self.modelo}") # funcion creada dentro de una clase


# ATRIBUTOS: son variables que perteneces a una clase
        
celular1 = Celular("Apple", "iPhone X", "20px") # a esto se le llama crear un objeto (un objeto es una instancia de una clase)
print(celular1.marca)
print(celular1.modelo)
print(celular1.camara)

# METODOS: los metodos, basicamente son funciones(son llamadas asi, las creadas dentro de una clase)
# los metodos sirven para definir las acciones que puede hacer nuestro objeto 
 
print(celular1.llamar()) # accion

###########################################################################################################

"""
Clase: estudiante
Atributos: nombre, edad y grado
Metodo: estudiar() que imprima que el alumno está estudiando

"""

class Estudiante(): 

    def __init__(self, nombre: str, edad: int, grado: str):
        self.nombre = nombre
        self.edad = edad 
        self.grado = grado

    def estudiar(self):
        print(f"{self.nombre} estudiando...")
    
nombre = input("Ingrese su nombre completo: ").upper()
edad = int(input("Ingrese su edad: "))
grado = input("Ingrese su año y curso: ").strip()

estudiante = Estudiante(nombre, edad, grado)

print(f"DATOS DEL ESTUDIANTE:\n\n"
      f"Nombre: {estudiante.nombre}\n"  
      f"Edad: {estudiante.edad}\n"
      f"Grado: {estudiante.grado}\n"
)

while True:
    estudiar = input("Ingrese estudiar si está actualmente estudiando: ").lower()
    if estudiar == "estudiar": # va en comillas porque sino estaria comparando la misma varible y no tiene sentido
        estudiante.estudiar()


# decoradores.py 

# DECORADORES: son usados para el manejo de excepciones y validaciones de entrada
# agrega una funcion antes y despues 

def decorador(funcion): 
    
    def funcion_modificada():
        print("Antes de llamar a la funcion")
        funcion()
        print("Despues de llamar a la funcion")
    return funcion_modificada

@decorador 
def saludo():
    print("Hola, como andas?")

saludo()

# DECORADOR PROPERTY:

class Persona:

    def __init__(self, nombre, edad):
        self.__nombre = nombre
        self._edad = edad

    @property # es un getter, por esta funcion, no puedo obtener otro valor si quiero un nuevo nombre
    def nombre(self): # tampoco es necesario usar el get
        return self.__nombre 
    # property es un decorador que accede a una propiedad
    
    @nombre.setter # con setter puedo obtener un nombre nuevo aún asi teniendo property
    def nombre(self, nuevo_nombre):
        self.__nombre = nuevo_nombre
    # setters es un decorador que modifica a una propiedad
        
datos = Persona("Valentin", 25)
nombre = datos.nombre # aca va un corchete pero con la funcion property ya no es necesario, tampoco es necesario usar el get (nombre.get_nombre(), asi se veria sin el property)
print(nombre)
        
datos.nombre = "Pepe"
nombre = datos.nombre
print(nombre)


# encapsulamiento.py 

# ENCAPSULAMIENTO: 

class MiClase:

    def __init__(self):
        self._atributo_privado = "Valor" # self._(un guion bajo quiere decir que un atributo es privado)

objeto = MiClase()
print(objeto._atributo_privado) 


class MiClase1:

    def __init__(self):
        self.__abributo_privado = "Valor" # self._(dos guiones bajo quiere decir que es aún mas privado)

objeto = MiClase1()
print(objeto.__abributo_privado)

# GETTERS y SETTERS: acceden a los valores que pueden ser privados o muy privados

class Persona:

    def __init__(self, nombre, edad):
        self._nombre = nombre
        self._edad = edad

    def get_nombre(self):
        return self._nombre 

    def set_nombre(self, nuevo_nombre): # establezco un nuevo nombre con set
        self._nombre = nuevo_nombre # a nombre le establezco otro nuevo nombre
    
datos = Persona("Valentin", 25)
nombre = datos.get_nombre() # si es muy privado con get desde la clase me lo devuelve
#1
print(nombre) # me lo devuelve porque lo estoy llamando desde la clase (con get)
#2
print(datos._nombre) # si es privado me lo devuelve, si es muy privado no a no ser que lo llame como en la linea 32, en este estoy accediendo desde afuera de la clase
# en fin, si son metodos privados y quiero acceder a ellos, obviamente siempre necesito la funcion get

datos.set_nombre("Valentino")
nombre = datos.get_nombre()
print(nombre)


# herencias.py 

# HERENCIA SIMPLE: heredar de la clase padre (clase principal)

class Individuo():
    
    def __init__(self, nombre, edad, nacionalidad):
        self.nombre = nombre 
        self.edad = edad
        self.nacionalidad = nacionalidad

class Empleado(Individuo):

    def __init__(self, nombre, edad, nacionalidad, trabajo, salario): # ponemos los que ya tiene + los agregados
        super().__init__(nombre, edad, nacionalidad) # con el super, heredamos lo de la clase padre
        self.trabajo = trabajo # propiedad especifica de la clase empleado
        self.salario = salario # propiedad especifica de la clase empleado

# HERENCIA MULTIPLE: creamos dos clases independientes, sin heredad de persona hacia artista
        
class Personaa:
    
    def __init__(self, nombre, edad, nacionalidad):
        self.nombre = nombre 
        self.edad = edad
        self.nacionalidad = nacionalidad

class Artista:

    def __init__(self, habilidad):
        self.habilidad = habilidad
    
    def mostrar_habilidad(self):
        return f"Mi habilidad es: {self.habilidad}"


class EmpleadoArtista(Personaa, Artista): # a esta clase nueva, le heredamos los objetos de las dos anteriores
     
    def __init__(self, nombre, edad, nacionalidad, habilidad, salario, empresa):

        Personaa.__init__(self, nombre, edad, nacionalidad) # es como decir super(Persona)
        Artista.__init__(self, habilidad) # es como decir super(Artista)
        self.salario = salario
        self.empresa = empresa

    def mostrando_habilidad(self):

        return f"{super().mostrar_habilidad()}" # va el super para que herede de la clase padre, no con self porque sino hereda de si misma (por si se quiere cambiar el programa y no llame a su misma clase si hacemos un cambio)
    
    def presentarse(self):

        print(f"Hola soy {self.nombre}, tengo {self.edad} años de edad, soy {self.nacionalidad} y mi habilidad es {self.habilidad}") # se utiliza print porque el return devuelve de la funcion de arriba mostrar_habilidad() 


roberto = EmpleadoArtista("Roberto", "35", "argentino", "Cantar", "100000", "SA")
roberto.presentarse()

instancia = isinstance(roberto, Personaa) # Roberto es un objeto de la clase Persona
print(instancia)

herencia = issubclass(EmpleadoArtista, Artista) # EmpleadoArtista hereda de la clase Artista
print(herencia) # True or False, si es herencia o no

# MRO: Metodo de resolucion de orden.
# es el orden en el que python busca metodos y atributos en las clases
# utilizando super() python le consulta al MRO


class A():
    
    def hablar(self):
        print("Hablando desde A")

class B():
    
    def hablar(self):
        print("Hablando desde B")

class C():

    def hablar(self):
        print("Habland desde C")

class D(B, C): # D primero va a heredar de B y de C luego, si uso pass en C y D, hereda de la padre A
    
    def hablar(self):
        print("Hablando desde B")

d = D()
d.hablar()

###########################################################################################################

"""
Crear un sistema para una escuela. En este sistema, vamos a tener dos clases principales:
Persona: atributos nombre y edad y un metodo que imprima el nombre y la edad de la persona
Estudiante: heredará de la clase persona y tambien tendrá un atributo adicional: grado y un metodo que imprima el grado del estudiante  
"""

class Persona:

    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad    
    
    def datos(self):
        return f"Nombre: {self.nombre}\nEdad: {self.edad}"
        

nombre = input("Ingrese su nombre: ").capitalize()
edad = int(input("Ingrese su edad: "))

class Estudiante(Persona):

    def __init__(self, nombre, edad, grado):
        super().__init__(nombre, edad) # si va super no lleva self, si va Persona, saco el super y pongo el self con los atributos
        self.grado = grado

    def datos(self):
          return f"{super().datos()}\nGrado: {self.grado}"

grado = int(input("Ingrese su grado: "))

estudiante = Estudiante(nombre, edad, grado)
print(estudiante.datos())

###########################################################################################################

"""
Crear tres clases: Animal, Mamifero y Ave
La clase animal debe tener un metodo llamado comer
La clase mamifero debe tener un metodo llamado amamantar
La clase ave debe tener un metodo volar
Luego, crea una clase murcielago que herede mamifero y ave, y por lo tanto, debe ser capaz de amamantar y volar, ademas de comer
Por ultimo, juega con el orden de herencia de clases murcielago y observa como cambia el MRO y el comportamiento de los metodos al usar super()
"""

class Animal: # tipo real

    def comer(self):
        print("El animal está comiendo...")

class Mamifero(Animal):

    def amamantar(self):
        print("El animal está amamantando...")

class Ave(Animal):

    def volar(self):
        print("El animal está volando")

class Murcielago(Mamifero, Ave):
    pass


murcielago = Murcielago() # tipo declarado
murcielago.comer()
murcielago.amamantar()
murcielago.volar()
print(Murcielago.mro())

# POLIMORFISMO = enviar el mismo mensaje a los metodos pero que se comporten de manera diferente. Ejemplo: decirle a un perro que haga un sonido y decirle a un gato que haga un sonido. Ambos harán la misma funcion pero lo harian de forma diferente

# Polimorfismo de metodos

class Gato:

    def sonido(self):
        return "Miau"
    
class Perro:

    def sonido(self):
        return "Guau"
    
gato = Gato()
perro = Perro()

print(gato.sonido())
print(perro.sonido())


# Polimorfismo de funciones

class Gato2:
    def sonido(self):
        return "Miau"
    
class Perro2:
    def sonido(self):
        return "Guau"

def hacer_sonido(animal):
    print(animal.sonido())

gato = Gato2()
perro = Perro2()

hacer_sonido(perro)
hacer_sonido(gato)

# Duck typing
# Enlaces dinamicos y estaticos 
# Tipo real y declarado python

# metodos especiales

# METODOS ESPECIALES:

class Persona:
    
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

    def __str__(self): # para que me lo devuelva en forma de cadena, sino me imprime la clase y no los datos
        return f"Nombre: {self.nombre}\nEdad: {self.edad}"

    
valentin = Persona("Valentin", 25)
print(valentin)

###########################################################################################################

"""
Crear una fusion de juego:
El juego consiste en crear personajes y que esos personajes se puedan fusionar para formar personajes mas poderesos 
""" 


class Personaje():

    def __init__(self, nombre, fuerza, velocidad):
        self.nombre = nombre
        self.fuerza = fuerza
        self.velocidad = velocidad

    def __repr__(self):
        return f"{self.nombre} (Fuerza: {self.fuerza} Velocidad: {self.velocidad})"
    
    def __add__(self, otro_pj):
        nuevo_nombre = self.nombre + "/" + otro_pj.nombre
        nueva_fuerza = round(((self.fuerza + otro_pj.fuerza)/2)**1)
                        # primero entre () para que realice la suma, luego () para que divida y calcule el promedio, y despues ** para que lo potencie 
        nueva_velocidad = round(((self.velocidad + otro_pj.velocidad)/2)**1)
        return Personaje(nuevo_nombre, nueva_fuerza, nueva_velocidad)
    
goku = Personaje("Goku", 100, 100)
vegeta = Personaje("Vegeta", 99, 99)
jiren = Personaje("Jiren", 80, 80)

gogeta = goku + vegeta
jireta = gogeta + jiren
print(jireta)
        
# solid.py

# SRP: principio de resposabilidad unica (cada clase tiene su unica responsabilidad)

class TanqueDeCombustible:
    def __init__(self):
        self.combustible = 100

    def agregar_combustible(self, cantidad):
        self.combustible += cantidad # agregando nafta
    
    def obtener_combustible(self): # esto es un getter
        return self.combustible

    def usar_combustible(self, cantidad):
        self.combustible -= cantidad

class Auto():

    def __init__(self, tanque):
        self.posicion = 0
        self.tanque = tanque
        
    def mover(self, distancia):
        if self.tanque.obtener_combustible() >= distancia / 2: # cada 2 de distancia gastamos 1 de combustible 
            self.posicion += distancia # asi el auto se mueve 
            self.tanque.usar_combustible(distancia / 2) # para saber cuanto esta consumiendo el auto
            print("El auto se movió exitosamente")
        else:
            print("No hay suficiente combustible")
    
    def obtener_posicion(self):
        return self.posicion
    
tanque = TanqueDeCombustible()
auto = Auto(tanque) # le pasamos el tanque para que pueda usarlo

print(auto.obtener_posicion())
print(auto.mover(30))
print(auto.obtener_posicion())
print(auto.mover(40))
print(auto.obtener_posicion())
print(auto.mover(60))
print(auto.obtener_posicion())
print(auto.mover(100))
print(auto.obtener_posicion())

# OCP: principo de abierto/cerrado (clases, funciones, etc... tiene que estar abiertas para su extension pero cerradas para la modificacion)

class Notificador:

    def __init__(self, usuario, mensaje):
        self.usuario = usuario
        self.mensaje = mensaje
    
    def notificar(self):
        raise NotImplementedError # le estamos diciendo al programador que si o si tiene que crear la clase notificar

class NotificadorEmail(Notificador):
    def notificar(self):
        print(f"Enviando mensaje a {self.usuario.email}")

class NotificadorSMS(Notificador):
    def notificar(self):
        print(f"Enviando mensaje a {self.usuario.sms}")

# LSP: principio de sustitucion de Liskov (si a es clase de b, donde se use b, a deberia poder usarse tambien)
        
class Ave: # definimos todas las aves y despues subclases como por ejemplo, aves nadadoras/no nadadoras...
    pass

class AveVoladora(Ave):
    def volar(self):
        return "Puedo volar"

class AveNoVoladora(Ave):
    pass
    
# ISP: principip de segregacion de la interfaz (dice que ningun cliente debe depender de interfaces que no utiliza, es decir, tenemos que eliminar las dependencias que no vamos a usar)

from abc import ABC, abstractmethod

class Trabajador(ABC):

    @abstractmethod
    def trabajar(self):
        pass

class Comedor(ABC):

    @abstractmethod
    def comer(self):
        pass

class Durmiente(ABC):

    @abstractmethod
    def dormir(self):
        pass

class Humano(Trabajador, Comedor, Durmiente):
      
    def comer(self):
        print("El humano está comiendo")

    def trabajar(self):
        print("El humano está trabajando")

    def dormir(self):
        print("El humano está durmiendo")

class Robot(Trabajador):

    def trabajar(self):
        print("El robot está trabajando")
    
robot = Robot()
humano = Humano()

robot.trabajar()
humano.trabajar()

# DIP: principio de inversion de dependencia (no depender de implementaciones especificas, sino de depender de interfaces mas complejas)


from abc import ABC, abstractmethod

class VerificadorOrtografico(ABC):

    @abstractmethod
    def verificar_palabra(self, palabra):
        pass

class Diccionario(VerificadorOrtografico):

    def verificar_palabra(self, palabra):
         # logica para verificar palabra si está en el diccionario
        pass

class CorrectorOrtografico: # depende de la abstraccion del verificador ortografico

    def __init__(self, verificador):
        self.verificador = verificador

    def corregir_texto(self, texto):
        # usamos el verificador para corregir el texto, no el diccionario
        
###########################################################################################################
        
"""
CHATBOT:
Desarrollaru un chatbot en python, que nos pida que le digamos algo y tome eso que le decimos, analice el sentimiento y nos responda como nos sentimos
"""

#from textblob import Textblob: libreria par analizar sentimientos, extraccion de palabras claves, traduccion de texto

class AnalizadorDeSentimientos:

    def analizar_sentimientos(self, texto):
        analisis = TextBlob(texto)
        if analisis.sentiment.polarity > 0:
            return "positivo"
        elif analisis.sentiment.polarity == 0:
            return "neutral"
        else:
            return "negativo"
        
analizador = AnalizadorDeSentimientos()
resultado = analizador.analizar_sentimientos("Hola, como estas?")
print(resultado)
