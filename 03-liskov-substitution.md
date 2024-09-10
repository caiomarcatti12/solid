# L — Liskov Substitution Principle (Princípio da substituição de Liskov)

Este princípio diz respeito que uma classe derivada (Herança) deve ser substituível pela sua classe base.

```php
class Pai{
   private $nome = 'João Alexander Primeiro';
   public function getNome(){
      return $this->nome;
   }

}

class Filho extends Pai{
    private $nome = 'João Alexander Segundo';
}
```

Com esse exemplo podemos utilizar da seguinte forma.

```php
function mostrarResultado(Pai $objeto){
  echo $objeto->getNome();
}

mostrarResultado(new Pai()); /* Saída:  João Alexander Primeiro **/
mostrarResultado(new Filho()); /* Saída:  João Alexander Segundo **/
```

Nesse exemplo “Filho” é derivativo de “Pai”, devido a isso o principio de substituição esta bem colocado.


Um outro exemplo, é quando temos que obter uma “particularidade” do objeto. Então por padrão a Classe “Pai” pode dirigir, mas a classe filho precisa ter a “idade” minima de 16 anos.

```php
class Pai{
  private $idade;
  
  public function setIdade($idade){
    $this->idade = $idade;
  }

  public function podeDirigir(){

     if($this->idade < 16) return false;
     return true;
  }
  
}

class Filho extends Pai{
  public function podeDirigir(){

    if($this->idade < 18) throw new Exception('Não pode dirigir');

    return true;
  }
}
```

Com esse exemplo podemos utilizar da seguinte forma.

```php
function mostrarResultado(Pai $objeto){
  echo $objeto->podeDirigir();
}

$pai = new Pai();
$pai->setIdade(40);

mostrarResultado($pai); /* Saída:  true **/


$primogenito = new Filho();
$primogenito->setIdade(20);

mostrarResultado($primogenito); /* Saída:  true **/

/** mas nesse cenário temos uma violação! **/
$cacula = new Filho();
$cacula->setIdade(7);

mostrarResultado($cacula); /* Saída:  Exception **/
```

A violação do LSP ocorre aqui, pois no método "podeDirigir" além de substituir a ação esperada pelo método da classe “Pai” e lança uma exceção inesperada "Não pode dirigir".

Outra violação do LSP, é se o método em questão altera o “retorno” por exemplo, de um booleano para um inteiro.

O principio **LSP** nos permite usar o polimorfismo com mais confiança. Podemos chamar nossas classes derivadas referindo-se à sua classe base sem preocupações com resultados inesperados.

