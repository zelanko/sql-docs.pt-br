---
description: Caixa de diálogo da instalação do Visual FoxPro do ODBC
title: Caixa de diálogo instalação do ODBC do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2083f76300ed19e047b0a138aed6c65ecef4da3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340702"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Caixa de diálogo da instalação do Visual FoxPro do ODBC
A caixa de diálogo **configuração do ODBC do Visual FoxPro** permite que você adicione ou altere uma fonte de dados do Visual FoxPro.  
  
 Para baixar o driver, consulte [o site de download do driver ODBC do Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opções de caixa de diálogo  
 **Nome da fonte de dados**  
 Digite o nome que você deseja usar para a fonte de dados.  
  
 **Descrição**  
 Digite uma descrição para a fonte de dados.  
  
 **Tipo de banco de dados**  
 Permite que você escolha o tipo de banco de dados ao qual você deseja que sua fonte se conecte.  
  
 **Banco de dados do Visual FoxPro (. DBC**  
 Especifica que a fonte de dados se conecta a um [banco](../../odbc/microsoft/visual-foxpro-terminology.md) de dado do Visual FoxPro (arquivo. DBC) e a todas as tabelas e exibições locais no banco de dados.  
  
 **Diretório de tabela livre**  
 Especifica que a fonte de dados se conecta a um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). Todas as tabelas de [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) no mesmo diretório são ignoradas por funções de catálogo ODBC, como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ou [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). As tabelas de banco de dados podem ser acessadas usando instruções SQL SELECT enviadas por meio de [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Caminho**  
 Exibe o caminho e o nome do banco de dados ou o diretório de tabelas livres aos quais a fonte de dado se conecta.  
  
 **Procurar**  
 Permite pesquisar o sistema e a rede no banco de dados ou diretório no qual você deseja conectar-se à fonte.  
  
 **Opções**  
 Expande a caixa de diálogo para que você possa definir opções de driver ODBC do Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequência de agrupamento**  
 A sequência na qual os campos são classificados. As sequências padrão refletem as sequências com suporte na sua versão de idioma do sistema operacional. Para obter uma lista de sequências de agrupamento com suporte, consulte [set COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando essa caixa de seleção está marcada, o driver abre o banco de dados do Visual FoxPro exclusivamente quando você acessa os dados usando a fonte. Outros usuários não podem acessar o banco de dados ou as tabelas no banco de dados enquanto o banco de dados é aberto exclusivamente. As tabelas dentro do banco de dados aberto exclusivamente são abertas como compartilhadas. Para abrir uma tabela exclusivamente, use o comando [set Exclusive](../../odbc/microsoft/set-exclusive-command.md) . Essa caixa de seleção é desabilitada quando o **tipo de banco de dados** é definido como diretório de **tabela livre**.  
  
 **Nulo**  
 Determina se as colunas criadas com ALTER TABLE e CREATE TABLE permitem valores nulos. Se você definir NULL ON, INSERT-SQL inserirá um valor nulo em qualquer coluna não incluída em um INSERT-SQL... Cláusula VALUE. Um espaço em branco será inserido se NULL for OFF. Você também pode controlar essa opção por meio de uma cadeia de conexão passada como no código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Excluída**  
 Determina se as linhas marcadas como excluídas são retornadas. Você também pode controlar essa opção por meio de uma cadeia de conexão passada como no código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Buscar dados em segundo plano**  
 Determina se os registros serão buscados em segundo plano (busca progressiva) ou se o aplicativo aguardará até que todos os registros no conjunto de resultados sejam buscados.
