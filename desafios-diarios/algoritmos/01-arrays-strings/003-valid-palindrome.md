# Desafio 3 — Valid Palindrome (Palíndromo Válido)

**Plataforma:** LeetCode
**Dificuldade:** Easy
**Link:** [https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)
**Data:** ____-__-__

## Enunciado

Uma frase é um **palíndromo** se, após converter todas as letras maiúsculas para minúsculas e remover todos os caracteres não-alfanuméricos, ela se lê da mesma forma da esquerda para a direita e da direita para a esquerda.

### Exemplos:
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explicação: "amanaplanacanalpanama" é um palíndromo.

Input: s = "race a car"
Output: false
Explicação: "raceacar" não é um palíndromo.

Input: s = " "
Output: true
Explicação: String vazia é palíndromo.
```

## Dica de Abordagem

1. Limpe a string (remova caracteres especiais, converta para minúsculo)
2. Compare com a versão invertida — OU use dois ponteiros

## Minha Solução

```javascript
// Escreva sua solução aqui!

function isPalindrome(s) {
  // Sua implementação
}

// Testes
console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
console.log(isPalindrome("race a car")); // false
console.log(isPalindrome(" ")); // true
```

## Complexidade
- Tempo: O(?)
- Espaço: O(?)

## Aprendizados
```
[Preencha após resolver]
```
