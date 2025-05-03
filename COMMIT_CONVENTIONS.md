# 📚 Padrão de Commits 

Utilize os seguintes prefixos nos seus commits para manter o histórico limpo e organizado.

## Tipos de commits

| Tipo       | Descrição                                              |
|------------|--------------------------------------------------------|
| **feat**   | Nova funcionalidade ou recurso                        |
| **fix**    | Correção de bug                                        |
| **chore**  | Tarefas de manutenção (configs, dependências, etc.)    |
| **refactor** | Refatoração de código (sem alterar a funcionalidade)  |
| **docs**   | Alterações na documentação                             |
| **style**  | Mudanças de formatação, identação (semântico)          |
| **test**   | Adição ou ajuste de testes                             |
| **build**  | Alterações que afetam o build ou dependências          |
| **perf**   | Melhorias de performance                               |
| **ci**     | Configuração de integração contínua                    |

## Exemplos de commits

- `feat: Adicionar funcionalidade de login com autenticação OAuth`
- `fix: Corrigir erro de cálculo de desconto na página de checkout`
- `chore: Atualizar dependências do React para a versão mais recente`
- `docs: Atualizar README com instruções de deploy no Heroku`
- `refactor: Simplificar a lógica de validação do formulário de cadastro`
- `style: Ajustar espaçamento entre os botões na interface do usuário`
- `test: Adicionar testes unitários para a função de verificação de e-mail`
- `build: Configurar Webpack para otimizar a produção de arquivos`
- `perf: Melhorar a performance da busca no banco de dados com índices`
- `ci: Adicionar configuração do GitHub Actions para deploy automático`

## Regras

- Sempre inicie a mensagem com um dos tipos acima, seguido de `:` e uma descrição no imperativo.
- Exemplo correto:  
  `feat: Adicionar funcionalidade de upload de arquivos`
- Evite mensagens genéricas como "update" ou "ajustes".

---

🔗 **Referência oficial:** [conventionalcommits.org](https://www.conventionalcommits.org/pt-br/v1.0.0/)
