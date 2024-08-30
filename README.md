## SOLID

- Single Responsibility Principle (SRP)
O propósito desse princípio é garantir que uma classe tenha apenas uma responsabilidade e não seja responsável por múltiplas tarefas. Eu aplico esse princípio em meu código criando classes separadas para cada responsabilidade, por exemplo, uma classe para lidar com a lógica de negócios e outra para lidar com a persistência de dados.

```java
// Classe que viola o SRP
public class Usuario {
    public void salvar() {
        // lógica de negócios
        // persistência de dados
    }
}

// Classe que segue o SRP
public class Usuario {
    public void salvar() {
        // lógica de negócios
    }
}

public class UsuarioRepository {
    public void salvar(Usuario usuario) {
        // persistência de dados
    }
}
```


- Open/Closed Principle (OCP)
Esse princípio estabelece que uma classe deve ser aberta para extensão, mas fechada para modificação. Eu aplico esse princípio em meu código usando interfaces e classes abstratas para permitir a extensão de funcionalidades sem modificar o código existente.

```java
// Classe que viola o OCP
public class Pagamento {
    public void processar() {
        if (tipoPagamento == "cartao") {
            // lógica de processamento de cartão
        } else if (tipoPagamento == "boleto") {
            // lógica de processamento de boleto
        }
    }
}

// Classe que segue o OCP
public interface PagamentoProcessador {
    void processar();
}

public class CartaoPagamentoProcessador implements PagamentoProcessador {
    public void processar() {
        // lógica de processamento de cartão
    }
}

public class BoletoPagamentoProcessador implements PagamentoProcessador {
    public void processar() {
        // lógica de processamento de boleto
    }
}
```

- Liskov Substitution Principle (LSP)
O propósito desse princípio é garantir que uma subclasse possa ser substituída por sua superclasse sem afetar a funcionalidade do sistema. Eu aplico esse princípio em meu código criando subclasses que são substituíveis por suas superclasses.

```java
// Classe que viola o LSP
public class Animal {
    public void som() {
        System.out.println("O animal faz um som");
    }
}

public class Cachorro extends Animal {
    public void som() {
        System.out.println("O cachorro late");
    }
}

public class Gato extends Animal {
    public void som() {
        System.out.println("O gato mia");
    }
}

// Classe que segue o LSP
public abstract class Animal {
    public abstract void som();
}

public class Cachorro extends Animal {
    public void som() {
        System.out.println("O cachorro late");
    }
}

public class Gato extends Animal {
    public void som() {
        System.out.println("O gato mia");
    }
}
```

- Interface Segregation Principle (ISP)
Esse princípio estabelece que uma interface deve ser segregada em interfaces menores e mais específicas. Eu aplico esse princípio em meu código criando interfaces separadas para cada funcionalidade, em vez de ter uma interface grande e complexa.

```java
// Interface que viola o ISP
public interface Impressora {
    void imprimir();
    void digitalizar();
    void enviarPorEmail();
}

// Interface que segue o ISP
public interface Impressora {
    void imprimir();
}

public interface Digitalizador {
    void digitalizar();
}

public interface EnviadorPorEmail {
    void enviarPorEmail();
}
```

- Dependency Inversion Principle (DIP)
O propósito desse princípio é garantir que as dependências sejam invertidas, ou seja, que as classes de alto nível não dependam de classes de baixo nível. Eu aplico esse princípio em meu código usando injeção de dependências para fornecer as dependências necessárias às classes.

```java
// Classe que viola o DIP
public class Usuario {
    public void salvar() {
        // lógica de negócios
        // persistência de dados
    }
}

// Classe que segue o DIP
public class Usuario {
    private UsuarioRepository repository;

    public Usuario(UsuarioRepository repository) {
        this.repository = repository;
    }

    public void salvar() {
        // lógica de negócios
        repository.salvar(this);
    }
}
```

## DESIGN PATTERNS

- Padrão de design Factory
Eu aplico o padrão de design Factory em meu código criando uma classe Factory que é responsável por criar objetos de diferentes classes.

```java
public class UsuarioFactory {
    public static Usuario criarUsuario(String tipo) {
        if (tipo.equals("admin")) {
            return new Administrador();
        } else {
            return new UsuarioComum();
        }
    }
}
```

- Padrão de design Singleton
Eu aplico o padrão de design Singleton em meu código criando uma classe que garanta que apenas uma instância seja criada.


```java
public class Logger {
    private static Logger instancia;

    private Logger() {}

    public static Logger getInstancia() {
        if (instancia == null) {
            instancia = new Logger();
        }
        return instancia;
    }
}
```

- Padrão de design Observer
Eu aplico o padrão de design Observer em meu código criando uma classe que notifica os observadores quando um evento ocorre.

```java
public interface Observador {
    void notificar(String mensagem);
}

public class Usuario implements Observador {
    public void notificar(String mensagem) {
        System.out.println("Usuário notificado: " + mensagem);
    }
}

public class Notificador {
    private List<Observador> observadores;

    public void notificar(String mensagem) {
        for (Observador observador : observadores) {
            observador.notificar(mensagem);
        }
    }
}
```

## ARQUITETURA HEXAGONAL

- Propósito da arquitetura hexagonal
A arquitetura hexagonal é uma abordagem de design de software que visa separar a lógica de negócios da infraestrutura e da apresentação.

- Aplicação da arquitetura hexagonal
Eu aplico a arquitetura hexagonal em meu código criando uma camada de lógica de negócios que é separada da camada de infraestrutura e da camada de apresentação.

- Vantagens da arquitetura hexagonal 
A arquitetura hexagonal permite uma maior flexibilidade e manutenibilidade do sistema, além de facilitar a troca de tecnologias e frameworks.

![image](https://github.com/user-attachments/assets/063b546b-0394-4de7-a69a-2954df6737ac)

-FRAMEWORK = CONTROLLER/REPOSITORY, APPLICATION = SERVICE

De maneira geral, essa arquitetura visa sempre o uso de interfaces para abstrair ao maximo visando tornar o mais generico possivel

## KAFKA

- Propósito do Kafka
O Kafka é um sistema de mensagens distribuído que permite a publicação e subscrição de mensagens.

- Uso do Kafka
Eu uso o Kafka em meu código para criar um sistema de mensagens que permita a comunicação entre diferentes componentes do sistema.

- Vantagens do Kafka
O Kafka permite uma alta escalabilidade e flexibilidade, além de fornecer uma alta taxa de transferência de mensagens.

EXEMPLO DE ARQUITETURA COM KAFKA:
Em uma aplicação de processamento de pagamentos, Kafka pode ser usado como um sistema de mensagens para processar pagamentos em lote.

```
graph LR
    A[Aplicação] -->|Produzir mensagem|> B[Kafka Topic]
    B -->|Consumir mensagem|> C[Processador de Pagamentos]
    C -->|Processar pagamento|> D[Banco de Dados]
```

## AWS S3

- Propósito do AWS S3
O AWS S3 é um serviço de armazenamento de objetos que permite armazenar e recuperar grandes quantidades de dados.

- Uso do AWS S3
Eu uso o AWS S3 em meu código para armazenar e recuperar arquivos e outros objetos.

- Vantagens do AWS S3
O AWS S3 fornece uma alta escalabilidade e flexibilidade, além de fornecer uma alta taxa de transferência de dados.
