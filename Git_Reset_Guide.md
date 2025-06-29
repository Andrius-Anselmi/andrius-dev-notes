
# Guia para Limpar Commits Indesejados no Git

## Cenário
Este guia mostra como remover commits indesejados, como o commit de merge ou o commit da LICENSE, e limpar o histórico no Git sem afetar os commits bons.

## Passo 1: Verifique o Histórico Atual
Use o comando abaixo para ver a lista de commits no seu repositório:

```bash
git log --oneline
```

Isso vai mostrar algo como:

```
d5737d5 (HEAD -> main) Create LICENSE
ca2205d feat: Implementa endpoints REST para Jogador e Clube
dc814c8 feat: Configura integração com MySQL e variáveis de ambiente
e73017a feat: Criação da entidade Clube e relação OneToMany
5b9dfe8 feat: Criação da entidade Jogador e relação ManyToOne
8d7a0a1 Primeiro commit: estrutura inicial do projeto
```

## Passo 2: Decida Qual Commit Deseja Remover
Determine até onde você quer manter os commits. No seu caso, você deseja manter o commit `ca2205d`, onde os endpoints REST foram implementados. Os commits posteriores, como o da LICENSE e o merge, serão removidos.

## Passo 3: Usar `git reset --hard` para Remover Commits Indesejados
Agora, use o comando `reset` para voltar o HEAD para o commit desejado:

```bash
git reset --hard ca2205d
```

Isso vai voltar o HEAD para o commit `ca2205d`, removendo os commits posteriores (como o `d5737d5` da LICENSE e o `e809468` do merge) **localmente**.

## Passo 4: Atualize o Repositório no GitHub (Push Forçado)
Agora, atualize o repositório remoto com as mudanças:

```bash
git push --force
```

Isso vai sobrescrever o histórico no GitHub, garantindo que o commit da LICENSE e o merge sejam removidos no repositório remoto também.

## Passo 5: Confirme as Mudanças
Depois de fazer o push, confira se tudo está correto com o comando:

```bash
git log --oneline
```

O histórico agora deve estar limpo, com os commits que você deseja manter e sem os indesejados.

## Dicas Importantes:
- **`git reset --hard`** remove os commits localmente, então só use quando tiver certeza de que quer limpar o histórico.
- **`git push --force`** pode sobrescrever o histórico remoto, então tenha cuidado, especialmente em projetos colaborativos.
- **Se você só quer remover um commit específico**, mas não mexer no resto do histórico, pode usar `git rebase -i` (mas isso tem que ser feito com mais cuidado quando há commits de merge).

## Recapitulando:
1. Verifique o histórico com `git log --oneline`.
2. Escolha até onde quer voltar (por exemplo, `ca2205d`).
3. Use `git reset --hard` para voltar ao commit desejado.
4. Use `git push --force` para atualizar o GitHub.
5. Verifique as mudanças com `git log --oneline`.

## EXTRA
## Corrigir mensagem do commit 
Fez o commit, mas errou na hora de escrever, e ainda não fez o git push
```bash
git commit --amend -m "frase do commit"
git push 

```
