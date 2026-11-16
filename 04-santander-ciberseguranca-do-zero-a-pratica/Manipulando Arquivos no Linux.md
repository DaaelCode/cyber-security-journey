# Navegando pelo sistema de arquivos no Linux

No Linux, os arquivos e diretórios são organizados em uma estrutura hierárquica que começa na raiz (`/`).

## 1. Símbolos importantes

| Símbolo | Significado |
|---|---|
| `/` | Diretório raiz do sistema |
| `~` | Diretório pessoal do usuário |
| `.` | Diretório atual |
| `..` | Diretório imediatamente acima do atual (anterior) |

## 2. Navegação

| Comando | Função |
|---|---|
| `pwd` | Mostra o caminho completo do diretório atual |
| `ls` | Lista os arquivos e diretórios do local atual |
| `ls -la` | Lista também os itens ocultos, em formato detalhado |
| `ls \|(pipe) more` | Mostra a listagem por partes; `Enter` avança uma linha e `q` sai |
| `cd nome_da_pasta` | Entra em um diretório. |
| `cd ..` | Volta para o diretório pai (anterior) |
| `cd /` | Vai para a raiz do sistema |
| `cd ~` ou `cd` | Vai para o diretório pessoal do usuário |

Os caminhos podem ser:

- **Absolutos:** começam em `/` e indicam o caminho completo, independentemente do diretório atual. Exemplo: `/home/usuario/Downloads`.
- **Relativos:** utilizam o diretório atual como referência. Exemplo: `Downloads`.

## 3. Criação e remoção

| Comando | Função |
|---|---|
| `touch arquivo.txt` | Cria um arquivo vazio ou atualiza sua data de modificação, caso já exista. |
| `mkdir pasta` | Cria um diretório. |
| `rmdir pasta` | Remove um diretório vazio. |
| `rm arquivo.txt` | Remove um arquivo. |

**Atenção:** `rm` exclui arquivos sem enviá-los para a lixeira. Confira o caminho antes de executar. A opção `-r` permite remover diretórios e seu conteúdo e o `-f` força a remoção, ficando: `rm -rf`.

## 4. Pesquisa de arquivos

O comando `find` procura arquivos e diretórios a partir do local informado.

Exemplo: procurar um arquivo específico a partir do diretório atual:

```bash
find . -name "arquivo.txt"
```

Procurar arquivos com extensão `.pdf` dentro do diretório pessoal:

```bash
find ~ -name "*.pdf"
```

**Opções úteis:**

| Opção | Função |
|---|---|
| `-name` | Pesquisa pelo nome, diferenciando maiúsculas de minúsculas. |
| `-iname` | Pesquisa pelo nome, sem diferenciar maiúsculas de minúsculas. |
| `-type f` | Pesquisa somente arquivos. |
| `-type d` | Pesquisa somente diretórios. |

## 5. Ajuda dos comandos

| Recurso | Função |
|---|---|
| `comando --help` | Mostra uma ajuda resumida com opções e formas de uso, quando disponível. |
| `man comando` | Abre o manual detalhado do comando. Pressione `q` para sair. |

Exemplos:

```bash
ls --help
man find
```

**Observação:** `--help` é uma opção usada junto a um comando; `man` é o comando que abre a página de manual.

## 6. Observações

- O Linux diferencia letras maiúsculas de minúsculas (*case sensitive*): `Downloads` e `downloads` podem ser nomes diferentes.
- O diretório atual influencia os comandos que utilizam caminhos relativos.
- Não é necessário decorar todas as opções. É importante entender a finalidade dos comandos e consultar a ajuda quando necessário.

# Executando tarefas administrativas como root

## Conceitos e comandos

- `cat`: visualizar conteúdo de um arquivo.
- `sudo`: para usar benefícios de administrador.
- Definir uma senha para o root (usuário que por padrão já existe) usando:

```bash
sudo passwd root
```

Depois, usar `su` para logar como root:

```bash
su
```

**Importante:** depois de fazer as tarefas como root, voltar para o usuário comum usando:

```bash
su nome_do_usuario
```

# Gerenciando usuários no Linux

## Criando e excluindo usuários

Criar um usuário:

```bash
useradd nome_do_usuario
```

Excluir um usuário:

```bash
userdel -f nome_do_usuario
```

Quando criei o usuário, ele não criou a pasta pessoal. Para criar o usuário com diretório pessoal e cadastrar o nome completo:

```bash
useradd joao -m -c "João da Silva"
```

## Definindo senhas

Cadastrar uma senha:

```bash
passwd joao
```

Para redefinir a senha, utiliza-se o mesmo comando:

```bash
passwd joao
```

## Definindo o shell

Caso o usuário não tenha um shell padrão configurado, definir o Bash:

```bash
chsh -s /bin/bash joao
```

Também é possível especificar o shell diretamente durante a criação do usuário:

```bash
useradd joao -m -c "João da Silva" -s /bin/bash
```

## Modificando usuários

O comando `usermod` é utilizado para realizar alterações em contas existentes.

Exemplo:

```bash
usermod joao -s /bin/bash
```