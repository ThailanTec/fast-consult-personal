# Array & Slice

### Definição:

Um **array** em Go é uma estrutura de dados que contém um número fixo de elementos do mesmo tipo. O tamanho do array é parte do seu tipo, ou seja, o tipo do array em Go é **`[n]Tipo`**, onde `n` é o número de elementos no array.

Características Avançadas dos Arrays:

- **Tamanho fixo**: O tamanho do array é imutável. Não é possível redimensionar um array depois de criado.
- **Estrutura de Dados Contígua**: Arrays são alocados de forma contígua na memória, o que pode resultar em um desempenho mais eficiente para acessar elementos sequenciais.

### Declaração e Inicialização:

Você pode inicializar um array de várias formas:

```go
var arr1 [5]int        // Um array de 5 inteiros, todos inicializados com 0.
arr2 := [3]int{1, 2, 3} // Um array de 3 inteiros com valores explícitos.
arr3 := [...]int{1, 2, 3} // O compilador infere o tamanho do array.
```

### Passagem de Arrays para Funções:

Ao passar um array para uma função, Go **faz uma cópia do array**. Ou seja, a função não pode alterar o array original:

```go
func modificarArray(arr [3]int) {
    arr[0] = 100
}

func main() {
    arr := [3]int{1, 2, 3}
    modificarArray(arr)
    fmt.Println(arr) // [1 2 3] (não foi alterado)
}
```

Se você quiser passar uma referência ao array, você pode passar um ponteiro:

```go
func modificarArray(arr *[3]int) {
    arr[0] = 100
}

func main() {
    arr := [3]int{1, 2, 3}
    modificarArray(&arr)
    fmt.Println(arr) // [100 2 3] (foi alterado)
}
```

### Acessando Array & Slice (Prox. Capitulo)

Em Go, **arrays** têm um tamanho fixo e os dados são acessados diretamente por seus índices. O índice do primeiro elemento começa em `0`.

```go
package main

func main() {
	// Temos um array de tamanho 5, com 5 elementos
	arr := [5]int{10, 20, 30, 40, 50}

	fmt.Println(arr[0]) // 10 (primeiro elemento)
	fmt.Println(arr[4]) // 50 (último elemento)

	// Modificando um elemento
	// Como estamos trabalhando com array, ele vai substituir o dado
	// pelo que passamos naquele endereço do array(memoria)
	arr[2] = 22

	fmt.Println(arr)
}

```

### **Slicing de Arrays**

Embora os arrays em Go sejam de tamanho fixo, você pode usar **slices** para criar "subarrays" (partes) de um array. O operador `:` é usado para **slice** (fatiar) um array ou slice.

### Sintaxe de Slicing:

```go
array[start:end]
```

- **start**: índice de onde começa o slice (inclusive).
- **end**: índice de onde o slice termina (exclusive). O elemento na posição `end` **não** é incluído.

**Exemplo de Slicing com Arrays:**

```go
package main

import "fmt"

func main() {
	arr := [5]int{10, 20, 30, 40, 50}

	// Slice do índice 1 até o índice 3 (não inclui o índice 4)
	// arr [indiceInicial | Indice Final - 1]
	slice := arr[1:4]

	fmt.Println(slice) // [20 30 40]
}

```

- O **índice de início** (`start`) é inclusivo, ou seja, o primeiro elemento do slice é o `arr[start]`.
- O **índice de fim** (`end`) é exclusivo, ou seja, o último elemento do slice é `arr[end-1]`.

### **Acessando Dados de Slices**

### **Slices em Go:**

Um **slice** é um tipo mais flexível e poderoso do que um array. Ele "aponta" para um segmento de um array subjacente, mas pode ter seu tamanho e capacidade alterados dinamicamente.

```go
package main

import "fmt"

func main() {
    slice := []int{10, 20, 30, 40, 50}

    // Acessando elementos
    fmt.Println(slice[0])  // 10 (primeiro elemento)
    fmt.Println(slice[4])  // 50 (último elemento)

    // Modificando um elemento
    slice[2] = 35
    fmt.Println(slice)     // [10 20 35 40 50]
}
```

### **Slicing de Slices**

O uso do operador `:` para fatiar slices é muito semelhante ao uso com arrays. A diferença é que os slices são mais flexíveis, pois você pode ajustar seu tamanho e capacidade dinamicamente.

```go
slice[start:end]

```

- **start**: Índice inicial (inclusivo), o primeiro elemento no novo slice.
- **end**: Índice final (exclusivo), o último elemento no novo slice **não é incluído**.

```go
package main

import "fmt"

func main() {
	slice := []int{10, 20, 30, 40, 50}

	// Slice do índice 1 até o índice 3 (não inclui o índice 4)
	// Sempre pensar que o ultimo é -1, já que ele não exibe proximo dado
	subSlice := slice[1:4]

	fmt.Println(subSlice) // [20 30 40]
}

```

### **Slicing com Posições Omissas**

Em Go, você pode omitir o **índice inicial** e/ou o **índice final** para usar os valores padrão. Os valores padrão são:

- **Omissão do início**: O padrão é `0` (início do slice).
- **Omissão do fim**: O padrão é o **tamanho** do slice (o fim do slice).

### Exemplo de Slicing com Posições Omissas:

```go
package main

import "fmt"

func main() {
	slice := []int{10, 20, 30, 40, 50}

	// Omissão do índice de início (começa do início)
	// A partir do 0, mostra até o 3
	slice1 := slice[:3]

	fmt.Println(slice1)

	// Omissão do índice do fim (vai até o final do slice)
	// A partir do 2, mostra todos os demais
	slice2 := slice[2:]

	fmt.Println(slice2)

	// Omissão de todos
	// Mostra tudo pra todos
	slice3 := slice[:]

	fmt.Println(slice3)
}

```

### **Slicing e Capacidade**

Quando você cria um slice, ele tem uma **capacidade** que pode ser menor que seu tamanho atual. A capacidade define até onde o slice pode crescer antes de ser realocado. Ao usar o operador `append()` em um slice, o Go pode aumentar a capacidade de forma automática se necessário, o que pode gerar a criação de um novo array **subjacente**.

### **Usando `:`, `start:end` em Operações Avançadas**

### **Modificando o Slice com `append()`**

A função `append()` permite adicionar elementos a um slice, aumentando sua capacidade conforme necessário:

```go
package main

import "fmt"

func main() {
	slice := []int{10, 20, 30}

	// Adicionando um elemento
	slice = append(slice, 40)
	fmt.Println(slice) // [10 20 30 40]

	// Adicionando múltiplos elementos, lembrando que sempre precisa ser do mesmo tipo
	slice = append(slice, 50, 60)
	fmt.Println(slice) // [10 20 30 40 50 60]
}

```

### **Fatiamento de Slice com Capacidade e Tamanho**

Ao trabalhar com slices, é útil compreender como o tamanho (`len`) e a capacidade (`cap`) do slice afetam a manipulação de dados:

```go
package main

import "fmt"

func main() {
	slice := make([]int, 3, 5) // Slice com 3 elementos e capacidade 5
	fmt.Println(len(slice))    // 3 (tamanho atual)
	fmt.Println(cap(slice))    // 5 (capacidade do slice)

	slice = append(slice, 4, 5) // Adicionando mais elementos
	fmt.Println(len(slice))     // 5 (tamanho atual)
	fmt.Println(cap(slice))     // 5 (capacidade ainda é 5)
}

```

- **Arrays** têm um tamanho fixo e são acessados por índices. Para manipulação mais flexível de dados, normalmente utilizamos **slices**.
- **Slices** são baseados em arrays, mas oferecem flexibilidade em termos de tamanho e capacidade. O operador `:` (slicing) permite extrair subconjuntos de um array ou slice.
- Ao usar **slicing**, você pode omitir os índices de início e fim para obter slices com base nos valores padrão, como começar do início ou ir até o final.
- **append()** é utilizado para adicionar elementos a um slice, e você pode usar o **slice[:len(slice)]** ou **slice[:]** para acessar todo o slice.

Esses conceitos são fundamentais para trabalhar eficientemente com dados em Go, e o entendimento correto de como funcionam os slices e arrays pode fazer uma grande diferença no desempenho e na flexibilidade do seu código.

### Maps

### Definição:

Um **map** é uma coleção de pares chave-valor, onde as chaves são únicas, e os valores podem ser de qualquer tipo. O tipo de um map é declarado como `map[Chave]Valor`.

### Características Avançadas dos Maps:

- **Chaves Únicas**: Cada chave em um map é única. Tentativas de inserir um valor com uma chave existente substituirão o valor anterior.
- **Desempenho**: Maps têm **tempo de busca constante (O(1))**, o que os torna extremamente eficientes para buscas rápidas.
- **Não Ordenado**: A ordem de inserção dos elementos não é garantida. Quando você itera sobre um map, a ordem dos pares chave-valor será imprevisível.

**Declaração de maps & Inicialização:**

```go
m := map[string]int{"um": 1, "dois": 2} // Inicialização com valores
m2 := make(map[string]int)               // Inicialização vazia

```