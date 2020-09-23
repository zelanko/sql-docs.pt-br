---
title: azdata bdc hdfs reference
titleSuffix: SQL Server big data clusters
description: Use este artigo de referência para entender os comandos SQL na ferramenta azdata, especificamente os comandos bdc hdfs.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17cac3a31309402d01442b598785908cbf345bba
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733450"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata bdc hdfs status](reference-azdata-bdc-hdfs-status.md) | Comandos de status do serviço do hdfs.
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | O shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | Listar o status do arquivo ou diretório fornecido.
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | Determinar se existe um arquivo ou diretório.  Retornará True se existir; caso contrário, False.
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | Criar um diretório no caminho especificado.
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | Mover o arquivo ou caminho especificado para a localização especificada.
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | Criar o arquivo de texto na localização especificada.  Conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | Ler o conteúdo de um arquivo.  O deslocamento e o comprimento em bytes são parâmetros opcionais.
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | Remover um arquivo ou diretório.
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | Remover recursivamente um arquivo ou diretório.
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | Alterar a permissão no arquivo ou diretório especificado.
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | Alterar o proprietário ou o grupo do arquivo especificado.
[azdata bdc hdfs cp](#azdata-bdc-hdfs-cp) | Copie um arquivo ou diretório entre o computador local e o HDFS.
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | Gerenciar a montagem de armazenamentos remotos no HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
O shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>Exemplos
Iniciar o shell.
```bash
azdata bdc hdfs shell
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
Listar o status do arquivo ou diretório fornecido.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Exemplos
Status da lista
```bash
azdata bdc hdfs ls --path tmp/
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
O caminho para o status da lista.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
Determinar se existe um arquivo ou diretório.  Retornará True se existir; caso contrário, False.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Exemplos
Verifique se um arquivo ou um diretório existe.
```bash
azdata bdc hdfs exists --path tmp/
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Caminho para verificar a existência.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
Criar um diretório no caminho especificado.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>Exemplos
Criar diretório.
```bash
azdata bdc hdfs mkdir --path tmp/
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do diretório a ser criado.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
Mover o arquivo ou caminho especificado para a localização especificada.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Exemplos
Mover arquivo ou diretório.
```bash
azdata bdc hdfs mv --source-path tmp/ --target-path "dest/"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--source-path -s`
O diretório a ser movido.
#### `--target-path -t`
A localização para a qual movê-lo.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
Criar o arquivo de texto na localização especificada.  Conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>Exemplos
Criar arquivo.
```bash
azdata bdc hdfs create --path "tmp/test.txt" --data "This is a test."
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo que será criado.
#### `--data -d`
Conteúdo do arquivo.  Destinado a conteúdo de texto simples.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
Ler o conteúdo de um arquivo.  O deslocamento e o comprimento em bytes são parâmetros opcionais.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    
--length -l
```
### <a name="examples"></a>Exemplos
Ler arquivo.
```bash
azdata bdc hdfs cat --path "tmp/test.txt"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo a ser lido.
#### `--offset`
Número de deslocamentos de bytes dentro do arquivo a ser lido.
#### `--length -l`
Comprimento dos dados a serem lidos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
Remover um arquivo ou diretório.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Exemplos
Remover um arquivo ou diretório.
```bash
azdata bdc hdfs rm --path tmp/
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo a ser removido.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
Remover recursivamente um arquivo ou diretório.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>Exemplos
Remover diretório recursivamente.
```bash
azdata bdc hdfs rmr --path tmp/
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo a ser removido recursivamente.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
Alterar a permissão no arquivo ou diretório especificado.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Exemplos
Alterar a permissão do arquivo ou diretório.
```bash
azdata bdc hdfs chmod --permission 775 --path "tmp/test.txt"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo ou diretório no qual definir permissões.
#### `--permission`
Octetos de permissão a serem definidos.  Por exemplo, "775".
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
Alterar o proprietário ou o grupo do arquivo especificado.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      
--group -g
```
### <a name="examples"></a>Exemplos
Alterar o proprietário e o grupo.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path "tmp/test.txt"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--path -p`
Nome do arquivo ou diretório cujo proprietário será alterado.
#### `--owner`
O nome do proprietário a ser definido.
#### `--group -g`
Nome do grupo a ser definido.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-cp"></a>azdata bdc hdfs cp
Copie um arquivo ou diretório entre o computador local e o HDFS.  Se a entrada for um diretório, a árvore de diretório inteira será copiada.  Se o arquivo ou diretório de destino existir, o comando falhará.  Para especificar o do diretório HDFS remoto, prefixe o caminho com "hdfs:"
```bash
azdata bdc hdfs cp --from-path -f 
                   --to-path -t
```
### <a name="examples"></a>Exemplos
Copie um arquivo ou um diretório entre o computador local e o HDFS.
```bash
azdata bdc hdfs cp --from_path "tmp/test.txt" --to-path "hdfs:/user/me/test.txt"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--from-path -f`
Nome do caminho do qual copiar.  Prefixe o caminho com "hdfs:" para indicar um caminho HDFS.
#### `--to-path -t`
Nome do caminho para o qual copiar.  Prefixe o caminho com "hdfs:" para indicar um caminho HDFS.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](../install/deploy-install-azdata.md).
