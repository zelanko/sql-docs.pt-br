---
title: referência do HDFS do BDC azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do azdata BDC HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426176"
---
# <a name="azdata-bdc-hdfs"></a>HDFS do BDC do azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **HDFS do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Shell do HDFS do BDC do azdata](#azdata-bdc-hdfs-shell) | O Shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
[azdata do HDFS do BDC](#azdata-bdc-hdfs-ls) | Listar o status do arquivo ou diretório fornecido.
[o HDFS do BDC azdata existe](#azdata-bdc-hdfs-exists) | Determine se existe um arquivo ou diretório.  Retorna true se Exists e false caso contrário.
[mkdir azdata de HDFS do BDC](#azdata-bdc-hdfs-mkdir) | Crie um diretório no caminho especificado.
[azdata de HDFS do BDC para o MV](#azdata-bdc-hdfs-mv) | Mover o arquivo ou caminho especificado para o local especificado.
[criação do HDFS do BDC azdata](#azdata-bdc-hdfs-create) | Crie o arquivo de texto no local especificado.  O conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
[Cat azdata do HDFS do BDC](#azdata-bdc-hdfs-cat) | Ler o conteúdo de um arquivo.  O deslocamento e o comprimento em bytes são parâmetros opcionais.
[RM HDFS do azdata BDC](#azdata-bdc-hdfs-rm) | Remover um arquivo ou diretório.
[RMR azdata do HDFS do BDC](#azdata-bdc-hdfs-rmr) | Remover recursivamente um arquivo ou diretório.
[chmod do azdata BDC HDFS](#azdata-bdc-hdfs-chmod) | Alterar a permissão no arquivo ou diretório especificado.
[proprietário do azdata BDC HDFS](#azdata-bdc-hdfs-chown) | Alterar o proprietário ou o grupo do arquivo especificado.
[montagem do HDFS do BDC azdata](reference-azdata-bdc-hdfs-mount.md) | Gerenciar a montagem de armazenamentos remotos no HDFS.
## <a name="azdata-bdc-hdfs-shell"></a>Shell do HDFS do BDC do azdata
O Shell do HDFS é um shell de comando interativo simples para o sistema de arquivos HDFS.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>Exemplos
Inicie o Shell.
```bash
azdata bdc hdfs shell
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-ls"></a>azdata do HDFS do BDC
Listar o status do arquivo ou diretório fornecido.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>Exemplos
Status da lista
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
O caminho para o status da lista.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-exists"></a>o HDFS do BDC azdata existe
Determine se existe um arquivo ou diretório.  Retorna true se Exists e false caso contrário.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>Exemplos
Verifique se há uma existência de arquivo ou de diretório.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Caminho para verificar a existência.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mkdir"></a>mkdir azdata de HDFS do BDC
Crie um diretório no caminho especificado.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>Exemplos
Criar diretório.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do diretório a ser criado.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-mv"></a>azdata de HDFS do BDC para o MV
Mover o arquivo ou caminho especificado para o local especificado.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>Exemplos
Mover arquivo ou diretório.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--source-path -s`
O diretório a ser movido.
#### `--target-path -t`
O local para o qual mover.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-create"></a>criação do HDFS do BDC azdata
Crie o arquivo de texto no local especificado.  O conteúdo de texto simples pode ser adicionado por meio do parâmetro de dados.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>Exemplos
Criar arquivo.
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser criado.
#### `--data -d`
Conteúdo do arquivo.  Destinado a conteúdo de texto simples.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-cat"></a>Cat azdata do HDFS do BDC
Ler o conteúdo de um arquivo.  O deslocamento e o comprimento em bytes são parâmetros opcionais.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>Exemplos
Ler arquivo.
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser lido.
#### `--offset`
O número de deslocamentos de bytes dentro do arquivo a ser lido.
#### `--length -l`
Comprimento dos dados a serem lidos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-rm"></a>RM HDFS do azdata BDC
Remover um arquivo ou diretório.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>Exemplos
Remover um arquivo ou diretório.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser removido.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-rmr"></a>RMR azdata do HDFS do BDC
Remover recursivamente um arquivo ou diretório.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>Exemplos
Remover diretório recursivo.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo a ser removido recursivamente.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-chmod"></a>chmod do azdata BDC HDFS
Alterar a permissão no arquivo ou diretório especificado.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>Exemplos
Altere a permissão de arquivo ou diretório.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo ou diretório no qual definir permissões.
#### `--permission`
Octetos de permissão a serem definidos.  Exemplo "775".
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-hdfs-chown"></a>proprietário do azdata BDC HDFS
Alterar o proprietário ou o grupo do arquivo especificado.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>Exemplos
Altere o proprietário e o grupo.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--path -p`
Nome do arquivo ou diretório do qual alterar o proprietário.
#### `--owner`
O nome do proprietário a ser definido como.
#### `--group -g`
Nome do grupo para o qual definir.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).
