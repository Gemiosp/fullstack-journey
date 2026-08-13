# Desafio 1 — Two Sum (Soma de Dois)

**Plataforma:** LeetCode
**Dificuldade:** Easy
**Link:** [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)
**Data:** ____-__-__

## Enunciado

Dado um array de números inteiros `nums` e um inteiro `target`, retorne os **índices** dos dois números que somam ao `target`.

Você pode assumir que cada entrada tem **exatamente uma solução**, e não pode usar o mesmo elemento duas vezes.

### Exemplos:
```
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explicação: nums[0] + nums[1] = 2 + 7 = 9

Input: nums = [3, 2, 4], target = 6
Output: [1, 2]
```

## Dica de Abordagem

Antes de olhar a solução, tente pensar:

1. **Força bruta:** Testar todos os pares (O(n²)) — funciona, mas é lento
2. **Otimizado:** Usar um Hash Map para armazenar valores já vistos (O(n))

## Minha Solução

```javascript
// Escreva sua solução aqui!

function twoSum(nums, target) {
  // Sua implementação
}

// Testes
console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1]
console.log(twoSum([3, 2, 4], 6));       // [1, 2]
console.log(twoSum([3, 3], 6));           // [0, 1]
```

## Complexidade
- Tempo: O(?)
- Espaço: O(?)

## Aprendizados
```
[Preencha após resolver]
```
