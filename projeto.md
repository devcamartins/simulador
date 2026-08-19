Crie um simulador interativo de um **pórtico de 4 rodas utilizando geometria de direção Ackermann**, onde **todas as dimensões do pórtico sejam configuráveis pelo usuário**.

### 1. Dimensões do pórtico

NÃO definir valores fixos para comprimento ou largura.

Criar campos de entrada para o usuário informar:

* Comprimento do pórtico (m)
* Largura do pórtico (m)
* Distância entre os eixos (m)
* Distância entre as rodas esquerda e direita (m)
* Posição das rodas dianteiras
* Posição das rodas traseiras

Exemplo de configuração:

```text
Comprimento: [      ] m
Largura:     [      ] m

Distância entre eixos: [      ] m
Bitola dianteira:      [      ] m
Bitola traseira:       [      ] m
```

Se o usuário informar apenas comprimento e largura, o sistema deve sugerir automaticamente posições iniciais para as rodas, mas permitir que elas sejam alteradas.

### 2. Representação

Mostrar o pórtico em uma visão superior 2D.

Representar:

* Chassi
* 4 rodas
* eixo central
* eixo dianteiro
* eixo traseiro
* centro geométrico
* centro instantâneo de rotação (ICR)
* trajetória
* raio da curva

As dimensões devem aparecer no desenho em metros.

### 3. Rodas

Identificar as rodas como:

```text
FL = Front Left
FR = Front Right

RL = Rear Left
RR = Rear Right
```

Cada roda deve possuir:

* posição X/Y;
* ângulo calculado;
* ângulo aplicado;
* limite máximo;
* limite mínimo.

### 4. Limitação individual dos ângulos

Permitir configurar individualmente o limite de cada roda.

Exemplo:

```text
FL:
Mínimo: [-45°]
Máximo: [45°]

FR:
Mínimo: [-45°]
Máximo: [45°]

RL:
Mínimo: [-45°]
Máximo: [45°]

RR:
Mínimo: [-45°]
Máximo: [45°]
```

Também criar uma opção:

```text
☐ Usar limite global

Limite: ±30°
```

Quando o cálculo exigir um ângulo acima do limite, o sistema deve aplicar o limite e informar que a roda foi limitada.

### 5. Raio da curva

Criar um campo:

```text
Raio desejado: [       ] m
```

Ao alterar o raio, recalcular automaticamente os ângulos das quatro rodas.

Mostrar:

```text
Raio desejado: 20.00 m

FL: 32.45°
FR: 27.81°
RL: ...
RR: ...
```

### 6. Ackermann

Implementar a geometria Ackermann considerando a **posição real de cada uma das quatro rodas**.

Não utilizar simplesmente o mesmo ângulo para todas as rodas.

As rodas devem apontar para o centro instantâneo de rotação correspondente à curva.

O sistema deve calcular:

* ICR;
* distância de cada roda ao ICR;
* ângulo necessário de cada roda;
* raio individual de cada roda;
* trajetória de cada roda.

### 7. Verificação dos limites

Depois de calcular os ângulos ideais, comparar com os limites configurados.

Exemplo:

```text
FL
Ideal: 38.4°
Limite: 30°
Aplicado: 30°
Status: LIMITADO
```

Se todas as rodas puderem atingir os ângulos necessários:

```text
Status: ACKERMANN OK
```

Se alguma roda atingir o limite:

```text
⚠ ACKERMANN LIMITADO
```

Mostrar também a trajetória ideal e a trajetória efetivamente possível.

### 8. Controle da direção

Adicionar:

```text
Direção:

○ Reta
○ Curva esquerda
○ Curva direita
○ Manual
```

Na curva esquerda, calcular automaticamente os ângulos.

Na curva direita, inverter corretamente a geometria.

No modo manual, permitir controlar cada roda individualmente através de sliders.

### 9. Simulação

Adicionar:

```text
▶ Iniciar
⏸ Pausar
↻ Resetar
```

Controle de velocidade:

```text
Velocidade: [ 0.0 ] m/s
```

O pórtico deve se movimentar pela trajetória calculada.

As rodas devem girar visualmente conforme os ângulos calculados.

### 10. Interface de configuração

Criar uma área chamada:

**CONFIGURAÇÃO DO PÓRTICO**

Com:

```text
Comprimento:       [     ] m
Largura:           [     ] m

Distância entre eixos:
                   [     ] m

Bitola dianteira:
                   [     ] m

Bitola traseira:
                   [     ] m
```

E uma área:

**LIMITES DAS RODAS**

```text
FL   Min [    ]°   Max [    ]°
FR   Min [    ]°   Max [    ]°
RL   Min [    ]°   Max [    ]°
RR   Min [    ]°   Max [    ]°
```

### 11. Visualização

O simulador deve atualizar o desenho em tempo real quando o usuário alterar:

* comprimento;
* largura;
* distância entre eixos;
* bitola;
* posição das rodas;
* raio;
* limites dos ângulos.

Adicionar:

* grid;
* escala;
* medidas;
* zoom;
* pan;
* eixo X/Y;
* ICR;
* linhas das rodas;
* trajetória.

### 12. Estrutura matemática

Separar a lógica matemática da interface.

Criar funções para:

```text
calculateWheelPositions()
calculateICR()
calculateWheelAngles()
calculateAckermann()
applyAngleLimits()
calculateTrajectory()
checkConstraints()
```

O cálculo deve trabalhar com qualquer dimensão fornecida pelo usuário.

Por exemplo, o usuário pode colocar:

```text
Comprimento = 14 m
Largura = 6 m
```

ou:

```text
Comprimento = 8 m
Largura = 4 m
```

ou:

```text
Comprimento = 20 m
Largura = 10 m
```

O simulador deve recalcular tudo automaticamente.

### 13. Objetivo principal

Quero que o resultado seja uma ferramenta de engenharia para testar diferentes configurações de um **pórtico de 4 rodas**, permitindo descobrir:

1. Qual ângulo cada roda precisa assumir para determinado raio.
2. Qual é o centro instantâneo de rotação.
3. Se os limites mecânicos das rodas permitem executar a curva.
4. Qual será a trajetória de cada roda.
5. O que acontece quando uma ou mais rodas atingem seu limite de direção.

Não utilizar dimensões fixas no código. **Comprimento, largura, distância entre eixos, bitolas e limites dos ângulos devem ser parâmetros configuráveis pelo usuário.**
