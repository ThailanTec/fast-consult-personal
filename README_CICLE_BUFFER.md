# Circular Buffer

É uma estrutura de dados que utiliza um único bloco de memória como se fosse um anel, permitindo o armazenamento e recuperação de dados de forma eficiente e continua. 

**Como funciona**

Imagine um **Array** com um número fixo de posições. Em um buffer circular, quando a última posição é alcançada, próximo elemento é armazenado na primeira posição, criando um  “loop” circular. Isso elimina a necessidade de realocar memória ou mover elementos quando o buffer está cheio, tornando-o ideal pra situações onde a velocidade e a eficiência são cruciais. 

**Principais Caracteristicas**

- **Tamanho fixo:** O buffer circular possui um tamanho predefinido, o que significa que ele só pode armazenar um número limitado de elementos.
- **Ponteiros de Letiura e Escrita**: Dois ponteiros, geralmente chamados de  “head” (cabeça”) e “tail” (Cauda), rastreiam a posição do próximo elemento a ser lido e escrito, respectivamente.
- **Comportamento FIFO**: Os elementos são removidos do buffer na mesma ordem em que foram adicionados, seguindo o principio FIFO.
- **Eficiência**: A inserção e removação de elementos em buffer circular têm camplexidade de tempo constante O(1), o que torna muito eficiente para aplicação em tempo real.

**Vantagens**

- **Eficiência em Tempo Real**: ideal para aplicações que exigem processamento rápido de dados, como streaming de áudio e video, comunicação de rede e sistemas embarcados.
- **Reutilização de memória**: Evita a necessidade de alocação de e desalocação constante de memória, reduzindo a sobrecarga do sistema.
- **Implementação Simples**: A lógica por trtás de buffer circular é relativamente simples de entender e implementar.

**Desvantagens**

- **Tamanho Fixo**: O tamanho limitado por ser um problema se a quantidade de dados a serem armazenadas  exceder a capacidade do buffer.
- **Sobrescrita de Dados**: Se o buffer ficar cheio e novos dados forem inseridos, os dados mais antigos serão sobrescritos, o que pode levar a perda de informações.

### Código de exemplo

```go
package main

import (
	"errors"
	"fmt"
)

type CircularBuffer struct {
	buffer []int
	size   int
	head   int
	tail   int
	full   bool
}

// NewCircularBuffer cria um novo buffer circular com um tamanho definido
func NewCircularBuffer(size int) *CircularBuffer {
	return &CircularBuffer{
		buffer: make([]int, size),
		size:   size,
		head:   0,
		tail:   0,
		full:   false,
	}
}

// Write adiciona um valor ao buffer
func (cb *CircularBuffer) Write(value int) error {
	if cb.full {
		// Sobrescreve o dado mais antigo (avança o ponteiro tail)
		cb.tail = (cb.tail + 1) % cb.size
	}

	cb.buffer[cb.head] = value
	cb.head = (cb.head + 1) % cb.size

	// Se head e tail coincidirem, o buffer está cheio
	cb.full = cb.head == cb.tail

	return nil
}

// Read lê e remove o valor mais antigo do buffer
func (cb *CircularBuffer) Read() (int, error) {
	if !cb.full && cb.head == cb.tail {
		return 0, errors.New("o buffer está vazio")
	}

	value := cb.buffer[cb.tail]
	cb.tail = (cb.tail + 1) % cb.size

	cb.full = false // Após a leitura, o buffer não está mais cheio
	return value, nil
}

// IsFull verifica se o buffer está cheio
func (cb *CircularBuffer) IsFull() bool {
	return cb.full
}

// IsEmpty verifica se o buffer está vazio
func (cb *CircularBuffer) IsEmpty() bool {
	return !cb.full && cb.head == cb.tail
}

// Exemplo de uso
func main() {
	cb := NewCircularBuffer(5)

	// Escrevendo dados no buffer
	cb.Write(10)
	cb.Write(20)
	cb.Write(30)
	cb.Write(40)
	cb.Write(50)

	// Excedendo o tamanho do buffer (substitui o mais antigo)
	cb.Write(60)

	// Lendo dados do buffer
	for !cb.IsEmpty() {
		value, _ := cb.Read()
		fmt.Println(value)
	}
}

```

**Detalhes da implementação sobre o código:** 

```go
if cb.full {
		// Sobrescreve o dado mais antigo (avança o ponteiro tail)
		cb.tail = (cb.tail + 1) % cb.size
	}
```

O operadador de módulo é usado para “enrolar” o inidica quando ele atingo o final do buffer. Em termos simples: 

- Se `cb.tail` for o último indice do buffer (`size - 1`), a soma de cb.tail + 1 excederá o tamanho do buffer.
- O módulo (`% cb.size`) garante que o indice volte para o inicio (indice 0) ao invés de sair dos limites do array.

Por exemplo: 

- Se `cb.size = 5` (buffer com tamanho 5) e `cb.tail = 4`:
    - `cb.tail + 1 = 5`.
    - `5 % 5 = 0` (volta para o início do buffer).

### **3. Atualização de** `cb.tail`**:**

```go
`cb.tail = (cb.tail + 1) % cb.size`
```

O resultado da operação `(cb.tail + 1) % cb.size` é atribuído de volta ao `cb.tail`, atualizando o índice para o próximo elemento no buffer circular.

- Vamos visualizar o comportamento com um buffer de tamanho `5` e o valor inicial de `tail` como `4`:
    - Após a atualização:
        - `(cb.tail + 1) % cb.size = (4 + 1) % 5 = 0`
        - `cb.tail = 0` (o ponteiro volta para o início do buffer).