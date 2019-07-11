---
title: referência de hdfs mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência de comandos do hdfs mssqlctl.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8f211faf827bdf925a8fde938fff8f96998bc359
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728535"
---
# <a name="mssqlctl-hdfs"></a>mssqlctl hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **hdfs** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[shell do hdfs mssqlctl](#mssqlctl-hdfs-shell) | O shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
[mssqlctl hdfs ls](#mssqlctl-hdfs-ls) | Liste o status de determinado arquivo ou diretório.
[hdfs mssqlctl existe](#mssqlctl-hdfs-exists) | Determine se existe um arquivo ou diretório.  Retorna True se existe e False caso contrário.
[mssqlctl hdfs mkdir](#mssqlctl-hdfs-mkdir) | Crie um diretório no caminho especificado.
[mssqlctl hdfs mv](#mssqlctl-hdfs-mv) | Mova o arquivo especificado ou o caminho para o local especificado.
[Criar mssqlctl hdfs](#mssqlctl-hdfs-create) | Crie o arquivo de texto no local especificado.  Conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
[hdfs mssqlctl ler](#mssqlctl-hdfs-read) | Ler o conteúdo de um arquivo.  Deslocamento e comprimento em bytes são parâmetros opcionais.
[mssqlctl hdfs rm](#mssqlctl-hdfs-rm) | Remova um arquivo ou diretório.
[mssqlctl hdfs rmr](#mssqlctl-hdfs-rmr) | Removem recursivamente um arquivo ou diretório.
[mssqlctl hdfs chmod](#mssqlctl-hdfs-chmod) | Altere a permissão no arquivo ou diretório especificado.
[mssqlctl hdfs chown](#mssqlctl-hdfs-chown) | Altere o proprietário ou o grupo do arquivo especificado.
## <a name="mssqlctl-hdfs-shell"></a>mssqlctl hdfs shell
O shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
```bash
mssqlctl hdfs shell 
```
### <a name="examples"></a>Exemplos
Inicie o shell.
```bash
mssqlctl hdfs shell
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-ls"></a>mssqlctl hdfs ls
Liste o status de determinado arquivo ou diretório.
```bash
mssqlctl hdfs ls --path -p 
                 
```
### <a name="examples"></a>Exemplos
Status da lista
```bash
mssqlctl hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho para o status da lista.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-exists"></a>hdfs mssqlctl existe
Determine se existe um arquivo ou diretório.  Retorna True se existe e False caso contrário.
```bash
mssqlctl hdfs exists --path -p 
                     
```
### <a name="examples"></a>Exemplos
Verificação de existência do arquivo ou diretório.
```bash
mssqlctl hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Caminho para verificar existência.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-mkdir"></a>mssqlctl hdfs mkdir
Crie um diretório no caminho especificado.
```bash
mssqlctl hdfs mkdir --path -p 
                    
```
### <a name="examples"></a>Exemplos
Torne o diretório.
```bash
mssqlctl hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do diretório a ser criado.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-mv"></a>mssqlctl hdfs mv
Mova o arquivo especificado ou o caminho para o local especificado.
```bash
mssqlctl hdfs mv --source-path -s 
                 --target-path -t
```
### <a name="examples"></a>Exemplos
Mova o arquivo ou diretório.
```bash
mssqlctl hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--source-path -s`
O diretório a ser movido.
#### `--target-path -t`
O local para mover para.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-create"></a>Criar mssqlctl hdfs
Crie o arquivo de texto no local especificado.  Conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
```bash
mssqlctl hdfs create --path -p 
                     --data -d
```
### <a name="examples"></a>Exemplos
Crie o arquivo.
```bash
mssqlctl hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser criado.
#### `--data -d`
Conteúdo do arquivo.  Deve-se para o conteúdo de texto simples.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-read"></a>hdfs mssqlctl ler
Ler o conteúdo de um arquivo.  Deslocamento e comprimento em bytes são parâmetros opcionais.
```bash
mssqlctl hdfs read --path -p 
                   --offset  
                   --length -l
```
### <a name="examples"></a>Exemplos
Leia o arquivo.
```bash
mssqlctl hdfs read --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser lido.
#### `--offset`
Número de bytes de deslocamento dentro do arquivo para leitura.
#### `--length -l`
Comprimento dos dados a serem lidos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-rm"></a>mssqlctl hdfs rm
Remova um arquivo ou diretório.
```bash
mssqlctl hdfs rm --path -p 
                 
```
### <a name="examples"></a>Exemplos
Remova um arquivo ou diretório.
```bash
mssqlctl hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser removido.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-rmr"></a>mssqlctl hdfs rmr
Removem recursivamente um arquivo ou diretório.
```bash
mssqlctl hdfs rmr --path -p 
                  
```
### <a name="examples"></a>Exemplos
Diretório de remover recursiva.
```bash
mssqlctl hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser removido recursivamente.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-chmod"></a>mssqlctl hdfs chmod
Altere a permissão no arquivo ou diretório especificado.
```bash
mssqlctl hdfs chmod --path -p 
                    --permission
```
### <a name="examples"></a>Exemplos
Alterar permissão de arquivo ou diretório.
```bash
mssqlctl hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo ou diretório para definir permissões em.
#### `--permission`
Octetos de permissão para definir.  Exemplo "775".
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-hdfs-chown"></a>mssqlctl hdfs chown
Altere o proprietário ou o grupo do arquivo especificado.
```bash
mssqlctl hdfs chown --path -p 
                    --owner  
                    --group -g
```
### <a name="examples"></a>Exemplos
Altere o proprietário e o grupo.
```bash
mssqlctl hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo ou diretório para alterar o proprietário do.
#### `--owner`
O nome do proprietário para definir como.
#### `--group -g`
Nome do grupo para definir como.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).