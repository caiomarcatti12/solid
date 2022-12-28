# D — Dependency Inversion Principle (Princípio da inversão da dependência)

Este princípio diz respeito à depender de uma abstração e não de uma implementação concreta.

Nesse caso, todos os demais princípios são aplicados, garantindo que os sistemas sejam o mais desacoplados e coesos possível.

Para isso, recomenda-se trabalhar com a inversão de dependências. Em linhas gerais, “inverter” uma dependência, nada mais é que passar uma classe (habitualmente uma classe interface) que será utilizada, para outra que irá consumir seus recursos.

### Exemplo de uma classe engessada

```php
class Pedido{
  public function recuperarPedido(){
      $conexao = new ConexaoMysql();
      /** faz alguma coisa com a conexão do banco de dados **/
  }
}
```

A classe acima esta totalmente engessada com a conexão com banco de dados mysql, assim dificultando uma troca de banco de dados por exemplo.

### Refatorando e trazendo a inversão de dependência

```php
/** Interface **/
interface ConexaoBD {
    public function connect();
}

/** Conexão com o banco MYSQL **/
class ConexaoMysql implements ConexaoBD {
   public function connect(){
    /** faz alguma coisa **/
   }
}

/** Conexão com o banco MongoDB **/
class ConexaoMongoDB implements ConexaoBD {
   public function connect(){
    /** faz alguma coisa **/
   }
}

/** Criação da classe Pedido com a abstração da interface **/
class Pedido{
  private $conexao;

  public function __construct(ConexaoBD $conexao){
    $this->conexao = $conexao;
  }

  public function recuperarPedido(){
  
      /** faz alguma coisa com a conexão do banco de dados **/
  }
}
```

Seguindo o exemplo de código acima, podemos instanciar a classe pedido, passando a responsabilidade de instanciar objeto do tipo **ConexaoBD** para a classe externa.

```php
/** Utilizando a conexão com Mysql na classe pedido **/
$conexaoMysql = new ConexaoMysql();
$pedido = new Pedido($conexaoMysql);

/** Utilizando a conexão com MongoDB na classe pedido **/
$conexaoMongoDB = new ConexaoMongoDB();
$pedido = new Pedido($conexaoMongoDB);
```


