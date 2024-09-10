# I — Interface Segregation Principle (Princípio da Segregação da Interface)

Este princípio diz respeito de segregar uma interface, ou seja, uma classe não deve ser forçada a ter um método “que não faz nada”. Então uma interface genérica esta fora de questão e com este principio trazemos coesão para as interfaces.

```php
interface Veiculo {
  public function ligar();
  public function executar();
  public function tanqueCheio();
}

class Moto implements Veiculo{
  public function ligar(){/** faz alguma coisa **/}
  public function executar(){/** faz alguma coisa **/}
  public function tanqueCheio(){/** faz alguma coisa **/}
}

class Bicicleta implements Veiculo{
  public function ligar(){/** não faz nada **/}
  public function executar(){/** faz alguma coisa **/}
  public function tanqueCheio(){/** não faz nada **/}
}
```

No exemplo acima a classe “Bicicleta” é obrigada a implementar os métodos “ligar” e “tanqueCheio”, pois a interface “Veiculo” é generalizada. Com essa implementação esses métodos não possuirão nenhum ação.

### Refatorando e trazendo coesão para interface

```php
interface Veiculo {
  public function executar();
}

interface VeiculoAutomotor extends Veiculo {
  public function ligar();
  public function tanqueCheio();
}

class Moto implements VeiculoAutomotor{
  public function ligar(){/** faz alguma coisa **/}
  public function executar(){/** faz alguma coisa **/}
  public function tanqueCheio(){/** faz alguma coisa **/}
}

class Bicicleta implements Veiculo{
  public function executar(){/** faz alguma coisa **/}
}
```

Dessa forma temos interfaces mais especificas que poderão ser usadas por mais de uma classe com comportamentos semelhantes.

