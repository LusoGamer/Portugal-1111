# Portugal 1111: A Conquista de Soure — Remover a verificação do CD (versão 1.12)

Este guia explica como modificar o executável da versão 1.12 de *Portugal 1111: A Conquista de Soure* para contornar a verificação do CD, utilizando um editor hexadecimal como o [HxD](https://mh-nexus.de/en/hxd/).

## 1. Preparação

Antes de começar:

- Faça uma cópia de segurança do executável original. (opcional)
- Confirme que está a utilizar a versão 1.12 do jogo.
- Abra uma cópia do executável num editor hexadecimal.
- Preserve o ficheiro original para poder restaurá-lo, se necessário.

## 2. Alterações necessárias

| Endereço | Offset no ficheiro | Bytes originais | Bytes modificados | Efeito |
|---|---|---|---|---|
| `0040369C` | `0x369C` | `74 40` | `EB 40` | Ignora a verificação do rótulo do volume do CD. |
| `00467F35` | `0x67F35` | `75 4A` | `EB 4A` | Contorna a verificação do ficheiro `CD.INI`. |

## 3. Procedimento no HxD

### 3.1. Contornar a verificação do rótulo do CD

1. Abra uma cópia do executável no HxD.
2. Abra a função de pesquisa de valores hexadecimais.
3. Procure a seguinte sequência:

   `74 40 6A 10 68 24 C9 4B 00`

4. Confirme que encontrou a sequência correta.
5. Altere o primeiro byte de `74` para `EB`, sem modificar os restantes bytes.

A sequência modificada será:

    EB 40 6A 10 68 24 C9 4B 00

### 3.2. Contornar a verificação do ficheiro CD.INI

1. Procure a seguinte sequência hexadecimal:

   `75 4A 8D 5E 14 8B 35 A0 C2 4B 00`

2. Confirme que encontrou a sequência correta.
3. Altere o primeiro byte de `75` para `EB`, sem modificar os restantes bytes.

A sequência modificada será:

    EB 4A 8D 5E 14 8B 35 A0 C2 4B 00

## 4. Guardar e testar

1. Guarde o executável modificado com um nome diferente do original.
2. Feche o HxD.
3. Execute o jogo utilizando o executável modificado.
4. Verifique se o jogo inicia e funciona corretamente.
5. Se ocorrerem erros, restaure a cópia de segurança.

## 5. Resumo das alterações

| Offset | Alteração |
|---|---|
| `0x369C` | `74 40` → `EB 40` |
| `0x67F35` | `75 4A` → `EB 4A` |

Estas alterações substituem instruções de salto condicional por saltos incondicionais, contornando as verificações descritas.

## 6. Notas finais

- As alterações destinam-se à versão 1.12 do jogo.
- Outras versões podem utilizar offsets ou sequências de bytes diferentes.
- É recomendado fazer uma cópia de segurança do executável original.

**Ferramenta recomendada:** [HxD — Editor hexadecimal](https://mh-nexus.de/en/hxd/)
