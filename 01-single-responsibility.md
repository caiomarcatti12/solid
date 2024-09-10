# S — Single Responsibility Principle (Princípio da responsabilidade única)

Esse princípio afirma que uma classe deve ser especializada em um único assunto e ter apenas uma responsabilidade dentro do software, ou seja, a classe deve ter uma única tarefa ou ação a realizar.

A princípio isso pode parecer eficaz, mas como os passivos acabam se misturando, quando houver a necessidade de fazer alterações nessa classe, será delicado modificar um desses passivos sem comprometer os demais.


### Exemplo de classe não coesa

```php
class Pedido {
  public function adicionarItem(){/** Faz algo **/}
  public function salvar(){/** Faz algo **/}
  private function calcularValores(){/** Faz algo **/}
  public function recuperarPedido(){/** Faz algo **/}
}
```

Essa classe generalizada é comum, além de lidar com diversas ações relacionadas ao pedido ela também altera o estado no banco de dados.

### Refatorando e trazendo coesão para classe

```php
/** Classe de manipulação do pedido **/
class Pedido {
  public function adicionarItem(){/** Faz algo **/}
  private function calcularValores(){/** Faz algo **/}
}

/** Classe de manipulação do pedido no banco de dados **/
class PedidoRepository {
  public function salvar(){/** Faz algo **/}
  public function recuperarPedido(){/** Faz algo **/}
}
```

### Podemos separar as responsabilidades em diferentes métodos?

Aqui optamos por dividir as responsabilidades em classes.

A pergunta é: será que poderíamos separar em métodos? O problema é justamente o reúso. Se quebrarmos um método grande em vários pequenos métodos privados, não teremos reúso daquele comportamento isolado.

Métodos privados são excelentes para melhorar a legibilidade de um método maior. Se você percebeu que existem duas diferentes responsabilidades em uma mesma classe, separe-os de verdade.

O princípio da responsabilidade única não se limita somente a classes, ele também pode ser aplicado em métodos e funções, ou seja, tudo que é responsável por executar uma ação, deve ser responsável por apenas aquilo que se propõe a fazer.

