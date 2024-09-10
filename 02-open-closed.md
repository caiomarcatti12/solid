# O — Open-Closed Principle (Princípio Aberto-Fechado)

Este princípio afirma que uma classe deve estar aberta para extensão, mas fechada para alteração.

Para contemplar este princípio utilizamos de abstrações e polimorfismo. Ao estender um novo comportamento em uma classe, devemos criar código novo e não alterar código existente.


### Exemplo de classe não coesa

```php
class Veículo{
  public function executar(){}/** faz algo aqui*/
}

class Moto extends Veículo {
  
}

class Carro extends Veículo
{
      
}

class Motorista {
  public function dirigir(Veiculo $veiculo){
    if($veiculo instanceof Moto){
      $this->ligarMoto();
    }
    if($veiculo instanceof Carro){
      $this->ligarCarro();
    }
    
    $veiculo->executar();
  }

  public function ligarMoto(){/** faz alguma coisa **/}

  public function ligarCarro(){/** faz alguma coisa **/}
}
```

No exemplo acima o método "dirigir" da classe "Motorista" precisará ser alterado sempre que for criado um novo tipo de veículo. Ou seja, ao adicionar um novo comportamento o código existente terá que ser alterado, indo totalmente contra o princípio do "Open/Closed"

### Refatorando e trazendo coesão com o principio

```php
abstract class Veículo{
  public function executar(){/** faz algo aqui */}
  abstract public function ligar();
}

class Moto extends Veículo {
  public function ligar(){/** faz algo aqui*/}
}

class Carro extends Veículo
{
  public function ligar(){/** faz algo aqui*/}
}

class Motorista {
  public function dirigir(Veiculo $veiculo){
    $veiculo->ligar();
    $veiculo->executar();
  }
}
```

No exemplo acima a classe "Veiculo" foi transformada em abstrata e o método "ligar" foi abstraído para a classes que estendem de "Veículo", desta forma, se criarmos um novo veículo, por exemplo "Trator", não será mais necessário alterar o código existente (método Motorista::dirigir), necessitando apenas que "Trator" estenda "Veiculo" e implemente o método "ligar".

