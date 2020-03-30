---
title: Cmdlet do PowerShell para avaliação de migração | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5272203fb1a1c0ac2f755a4da99c654b2595a7f0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68698311"
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>Cmdlet do PowerShell para Avaliação da Migração

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O cmdlet `Save-SqlMigrationReport` é uma ferramenta que avalia a adequação da migração de vários objetos em um banco de dados do SQL Server.

Atualmente, este cmdlet é limitado à avaliação da adequação da migração para o OLTP in-memory. O cmdlet pode ser executado em um ambiente do Windows PowerShell com privilégios elevados e no sqlps.

Como alternativa a executar esse cmdlet do PowerShell diretamente, você pode executar o cmdlet implicitamente usando o SSMS (SQL Server Management Studio). No **Pesquisador de Objetos** do SSMS, você pode clicar com o botão direito do mouse em uma tabela clicar em **Assistente de Otimização de Memória**.

## <a name="syntax"></a>Sintaxe

```
Save-SqlMigrationReport
    -FolderPath <output_path>
    [ -MigrationType <migration_scenario_type> ]
    [
        [ -Server <server_name> -Database <database_name>
            [ -Schema <schema_name> ] [ -Object <object_name> ]
        ]
       |
        [ -InputObject <smo_object> ]
    ]
;
```

## <a name="parameters"></a>parâmetros

A tabela a seguir descreve os parâmetros.

Há aspectos da sintaxe que precisam ser enfatizados. Se especificar o parâmetro `-InputObject`, você não poderá especificar nenhum dos seguintes parâmetros:

- `-Server`
- `-Database`
- `-Schema`
- `-Object`

Por outro lado, se _não_ especificar `-InputObject`, você deverá especificar `-Server` e `-Database`. Se especificar `-Server`, você terá a opção de restringir o escopo especificando `-Schema` ou `-Object`, ou ambos.

| Nome do parâmetro | Descrição |
| :------------- | :---------- |
| Banco de dados | O nome do banco de dados do SQL Server de destino. Obrigatório quando `-Server` é obrigatório.<br/><br/> Opcional no SQLPS. |
| FolderPath | A pasta em que o cmdlet deve armazenar os relatórios gerados.<br/><br/> Obrigatórios. |
| InputObject | O objeto SMO que o cmdlet deve ter como destino.<br/><br/> Obrigatório no ambiente do Windows Powershell se o parâmetro `-Server` não for fornecido.<br/><br/> Opcional no SQLPS. |
| MigrationType | O tipo de cenário de migração que o cmdlet tem como destino. Atualmente, o único valor é o **'OLTP'** padrão.<br/><br/> Opcional. |
| Objeto | O nome do objeto sobre o qual o relatório será feito. Pode ser uma tabela ou um procedimento armazenado. |
| Senha | Obrigatório quando o `-Username` for obrigatório. |
| Esquema | O nome do esquema que tem o objeto sobre o qual o relatório será feito.<br/><br/> Opcional. |
| Servidor | O nome da instância do SQL Server de destino. Obrigatório no ambiente do Windows Powershell se o parâmetro `-InputObject` não for fornecido.<br/><br/> Opcional no SQLPS. |
| Nome de Usuário | Obrigatório ao se conectar usando a Autenticação do SQL Server em vez da Autenticação do Windows. Caso contrário, omita. |
| &nbsp; | &nbsp; |

## <a name="prerequisites"></a>Pré-requisitos

Antes de executar este cmdlet, você precisa instalar o módulo chamado **SqlServer:**

- `Install-Module -Name SqlServer`

> [!NOTE]
> O módulo `SQLPS` antigo não está mais recebendo manutenção. Use o módulo `SqlServer` mais recente.

Para obter mais informações, consulte [Instalar o módulo do SQL Server PowerShell](../../powershell/download-sql-server-ps-module.md).

## <a name="example-cmdlet-line"></a>Linha de cmdlet de exemplo

A seguir, temos a linha do cmdlet real que foi executada para gerar o relatório exibido posteriormente neste artigo.

```powershell
Save-SqlMigrationReport `
  -FolderPath 'C:\Test\PowerShell-ps1\Save-SqlMigrationReport\' `
  -Server 'MyUserName123456.database.windows.net' `
  -Database 'MyDatabaseName_31' `
  -Schema 'dbo' `
  -Object 'Table2' `
  -Username 'MyUserName' `
  -Password 'MyPassword' `
  -MigrationType 'OLTP' `
;
```

## <a name="example-output-report"></a>Exemplo de relatório de saída

Na pasta especificada para o parâmetro `-FolderPath`, são criados os dois caminhos de pasta a seguir executando esse cmdlet. Os dois caminhos começam com o valor _nome do\_servidor_:

- MyDatabaseName_31\Tables\
- MyDatabaseName_31\Stored Procedures\

Cada arquivo de relatório de objeto é armazenado na pasta apropriada.

Os nomes dos arquivos de relatório têm a extensão **.html**. Por exemplo, um nome de arquivo gerado real foi **MigrationAdvisorChecklistReport_Table2_20190728.html**.

O HTML é basicamente uma tabela de duas colunas com os seguintes cabeçalhos:

- Descrição
- Resultado da Validação

A seguir, temos um exemplo real do relatório HTML de uma tabela.

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
  <head>
    <title>Memory optimization checklist for [MyDatabaseName_31].[Table2]</title>
  </head>
  <body>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 14pt;">
      <b>Memory optimization checklist for [MyDatabaseName_31].[Table2]</b>
    </p>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 10pt;">
      <b>Report Date/Time:</b>7/28/2019 2:25 PM<br /></p>
    <table border="1" cellpadding="5" cellspacing="0" STYLE="font-family: Verdana, Arial, sans-serif; font-size: 9pt;">
      <tr style="background-color:Silver">
        <th colspan="2" align="center">Description</th>
        <th align="center">Validation Result</th>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported data types are defined on this table. </td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No sparse columns are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No identity columns with unsupported seed and increment are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No foreign key relationships are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported constraints are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No unsupported indexes are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported triggers are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">Post migration row size does not exceed the row size limit of memory-optimized tables.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">Table is not partitioned or replicated.</td>
        <td>Succeeded</td>
      </tr>
    </table>
  </body>
</html>
```

E, em seguida, uma aproximação da aparência da tabela.

| Descrição | Resultado da Validação |
| :---------- | :---------------- |
| Não há tipos de dados sem suporte definidos nesta tabela. | Teve êxito |
| Não há colunas esparsas definidas para esta tabela. | Teve êxito |
| Não há nenhuma coluna de identidade com semente e incremento sem suporte definida para essa tabela. | Teve êxito |
| Não há relações de chave estrangeira definidas nesta tabela. | Teve êxito |
| Não há restrições sem suporte definidas nesta tabela. | Teve êxito |
| Não há índices sem suporte definidos nesta tabela. | Teve êxito |
| Não há gatilhos sem suporte definidos nesta tabela. | Teve êxito |
| O tamanho de linha após a migração não excede o limite de tamanho de linha de tabelas com otimização de memória. | Teve êxito |
| A tabela não está particionada nem replicada. | Teve êxito |
| &nbsp; | &nbsp; |

## <a name="related-links"></a>Links relacionados

- Documentação de referência: [Save-SqlMigrationReport](/powershell/module/sqlserver/save-sqlmigrationreport?view=sqlserver-ps)
