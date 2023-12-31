# Bash-Fu

O objetivo desta documentação é reunir algumas informações acerca de comandos importantes do linux, que são relevantes para o DevOps, que atuam na manipulação de texto e arquivos

## `pushd`

Permite mudar do diretório atual para o diretório designado e salvar simultaneamente o diretório anterior em uma pilha. É útil quando você deseja mudar temporariamente para um diretório diferente, mas planeja retornar ao diretório anterior mais tarde.

Exemplo:

```bash
user@server:~/original/directory$ pushd /new/directory
user@server:~/new/directory$
```

Opções:

- `-n`: Suprime a mudança normal de diretório ao adicionar diretórios à pilha, de forma que apenas a pilha seja manipulada.

Argumentos:

- `+N`: Gira a pilha para que o enésimo diretório (contando a partir da esquerda da lista mostrada por `dirs`, começando com zero) esteja no topo.
- `-N`: Gira a pilha para que o enésimo diretório (contando a partir da direita da lista mostrada por `dirs`, começando com zero) esteja no topo.
- `/new/directory`: Adiciona `/new/directory` à pilha de diretórios no topo, tornando-o o novo diretório de trabalho atual.

## `dirs` command

Exibe os diretórios salvos com `pushd`.

Exemplo:

```bash
user@server:~$ dirs
~/original/directory ~/new/directory
```

## `popd`

Usado para retornar a algum diretório salvo anteriormente com o `pushd`. Retira o diretório da pilha.

Exemplo:

```bash
user@server:~/new/directory$ popd
user@server:~/original/directory$
```

Opções:

- `-n`: Suprime a mudança normal de diretório ao remover diretórios da pilha, de forma que apenas a pilha seja manipulada.

Argumentos:

- `+N`: Remove a enésima contagem de entradas à esquerda da lista mostrada por `dirs`, começando com zero. Por exemplo: `popd +0` remove o primeiro diretório, `popd +1` o segundo.
- `-N`: Remove a enésima entrada contada à direita da lista mostrada por `dirs`, começando com zero. Por exemplo: `popd -0` remove o último diretório, `popd -1` o penúltimo.

## `grep`

Permite que você procure padrões em arquivos. Utilize `zgrep` para arquivos `.gzip`

Exemplo:

```bash
$ grep padrão-a-ser-encontrado file.log

padrão-a-ser-encontrado
```

Parâmetros:

- `-n`: número de linhas correspondentes.
- `-i`: ignorar maiúsculas e minúsculas (*case insensitive*).
- `-v`: Inverter correspondências, ou seja, selecionar linhas não correspondentes.
- `-E`: Regex extendido.
- `-c`: Contar o número de correspondências.
- `-l`: Encontrar nomes de arquivos que correspondam ao padrão.

## `ngrep`

Usados para analisar pacotes de rede.

Exemplo:

```bash
$ ngrep -q '.' 'icmp'

interface: enp0s3 (10.0.2.0/255.255.0)
filter: ( icmp ) and ((ip || ip6)) || (vlan && (ip || ip6)))
match: .
```

Parâmetros:

- `-d`: Especificar a interface de rede.
- `-i`: Ignorar diferença entre maiúsculas e minúsculas (*case insensitive*).
- `-x`: Printar em *hexdump* alternado.
- `-t`: Printar o *timestamp*.
- `-I`: Ler arquivo `.pcap`.

## `cut`

Usado para analisar campos de logs delimitados.

Exemplo:

```bash
$ cut -d ":" -f 2 file.env
VARIABLE value
```

Parâmetros:

- `-d`: Usar o delimitador de campo.
- `-f`: O número dos campos.
- `-c`: Especificar posição dos caracteres.

## `sed`

Usado para substituir *strings* em um arquivo.

Exemplo:

```bash
$ sed s/regex/replace/g
replace
```

Parâmetros:

- `s`: Pesquisar.
- `g`: Substituir.
- `d`: Deletar.
- `w`: Anexar ao arquivo.
- `-e`: Executar comando.
- `-n`: Suprimir saída.

## `sort`

Usado para ordenar as linhas de um arquivo.

Exemplo:

```bash
$ sort file.txt
1
2
3
```

Parâmetros:

- `-o`: Saída para o arquivo.
- `-r`: Ordem reversa.
- `-n`: Ordem numérica.
- `-k`: Ordenar por coluna.
- `-c`: Verificar se ordenado.
- `-u`: Ordenar e remover.
- `-f`: Ignorar diferenças entre maiúsculas e minúsculas (*case insensitive*).
- `-h`: Ordenar números em uma leitura amigável (*human readable*).

## `uniq`

É utilizado para remover ou reportar linhas duplicadas em um arquivo.

Exemplo:

```bash
$ uniq file.txt
unificada
```

Parâmetros:

- `-c`: Contar o número de duplicatas.
- `-d`: Printar duplicatas.
- `-i`: Ignorar diferenças entre maiúsculas e minúsculas (*case insensitive*).

## `diff`

Usado para mostrar as diferênças entre arquivos ao compará-los linha por linha.

Exemplo:

```bash
$ diff file1.txt file2.txt
2c2
< a
---
> b
```

Como fazer a leitura da saída do comando:

- `a`: Adicionar.
- `c`: Modificar.
- `d`: Deletar.
- `#`: Número das linhas.
- `<`: Referente ao primeiro arquivo.
- `>`: Referente ao segundo arquivo.

## `awk`

É uma linguagem de programação usada para manipular dados.

Exemplo:

```bash
$ awk {print $2} file.log
segunda_coluna
```

---

Printar a primeira coluna com separador ":"

```bash
awk -F: '{print$1}' /etc/passwd
primeira_coluna:
```

---

Extrair valor *uniq* de dois arquivos

```bash
awk 'FNR==NR {a[$0]++; next} !($0 in a)' file1.txt file2.txt
```

---
