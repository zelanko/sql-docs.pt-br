---
title: Caixa de diálogo de instalação do ODBC do Visual FoxPro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35e9da17a9c3980470cfd3dcbb22b4069afec640
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501749"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Caixa de diálogo da instalação do Visual FoxPro do ODBC
O **a instalação do Visual FoxPro ODBC** caixa de diálogo permite que você adicionar ou alterar uma fonte de dados do Visual FoxPro.  
  
 Para baixar o driver, consulte [o site de download do Driver ODBC do Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opções da caixa de diálogo  
 **Nome da fonte de dados**  
 Digite o nome que você deseja usar para a fonte de dados.  
  
 **Descrição**  
 Digite uma descrição para a fonte de dados.  
  
 **Tipo de banco de dados**  
 Permite que você escolha o tipo de banco de dados que você deseja que sua fonte de dados para se conectar ao.  
  
 **Banco de dados do Visual FoxPro (. DBC)**  
 Especifica que a fonte de dados se conecta a um Visual FoxPro [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) (arquivo. dbc) e para todas as tabelas e exibições locais no banco de dados.  
  
 **Diretório livre de tabela**  
 Especifica que a fonte de dados se conecta a um diretório da [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). Qualquer [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) tabelas no mesmo diretório, como são ignoradas pelas funções de catálogo ODBC [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ou [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Tabelas de banco de dados podem ser acessadas usando instruções SQL SELECT enviadas por meio [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Caminho**  
 Exibe o caminho e o nome para o banco de dados ou o diretório de tabelas livres ao qual a fonte de dados se conecta.  
  
 **Procurar**  
 Permite que você pesquise seu sistema e rede para o banco de dados ou o diretório ao qual você deseja se conectar à fonte de dados.  
  
 **Opções**  
 Expande a caixa de diálogo para que você pode definir opções de Driver de ODBC do Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequência de agrupamento**  
 A sequência na qual os campos são classificados. As sequências de padrão refletem as sequências compatíveis com sua versão de idioma do sistema operacional. Para obter uma lista de sequências de agrupamento com suporte, consulte [definir COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando essa caixa de seleção é selecionada, o driver abre o banco de dados do Visual FoxPro exclusivamente ao acessar dados usando a fonte de dados. Outros usuários não podem acessar o banco de dados ou as tabelas no banco de dados enquanto o banco de dados fica aberto exclusivamente. Tabelas no banco de dados aberto exclusivamente são abertas como compartilhado. Para abrir uma tabela de modo exclusivo, use o [exclusivo definido](../../odbc/microsoft/set-exclusive-command.md) comando. Essa caixa de seleção está desabilitada quando **tipo de banco de dados** é definido como **tabela livre**.  
  
 **Nulo**  
 Determina se as colunas com ALTER TABLE e CREATE TABLE permitirão valores nulos. Se você definir ON nulo, o INSERT - SQL insere um valor nulo em qualquer coluna que não são incluída em uma instrução INSERT - SQL... Cláusula VALUE. Um espaço em branco é inserido quando Null é OFF. Você também pode controlar essa opção por meio de uma cadeia de caracteres de conexão passada como no código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Excluído**  
 Determina se as linhas marcadas como excluídas são retornadas. Você também pode controlar essa opção por meio de uma cadeia de caracteres de conexão passada como no código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Buscar dados em segundo plano**  
 Determina se os registros serão buscados em segundo plano (buscando progressivo) ou seu aplicativo aguardará até que todos os registros no conjunto de resultados.
