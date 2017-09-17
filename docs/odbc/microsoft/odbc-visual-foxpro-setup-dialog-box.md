---
title: "Caixa de diálogo de configuração do ODBC do Visual FoxPro | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 22208bd706e7b8966f54a501e9580b35d99a0555
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Caixa de diálogo de configuração do ODBC do Visual FoxPro
O **a instalação do Visual FoxPro ODBC** caixa de diálogo permite que você adicionar ou alterar uma fonte de dados do Visual FoxPro.  
  
 Para baixar o driver, consulte [o site de download do Visual FoxPro ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opções da caixa de diálogo  
 **Nome da fonte de dados**  
 Digite o nome que você deseja usar para a fonte de dados.  
  
 **Description**  
 Digite uma descrição da fonte de dados.  
  
 **Tipo de banco de dados**  
 Permite que você escolha o tipo de banco de dados para conectar-se à sua fonte de dados.  
  
 **Banco de dados do Visual FoxPro (. DBC)**  
 Especifica que a fonte de dados se conecta a um Visual FoxPro [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) (arquivo. dbc) e para todas as tabelas e exibições locais no banco de dados.  
  
 **Diretório de tabela livre**  
 Especifica que a fonte de dados se conecta a um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md). Qualquer [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) tabelas no mesmo diretório são ignoradas por funções de catálogo ODBC como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ou [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Tabelas de banco de dados podem ser acessadas usando instruções SQL SELECT enviadas pelo [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Caminho**  
 Exibe o caminho e o nome para o banco de dados ou o diretório de tabelas livres que conecta a fonte de dados.  
  
 **Procurar**  
 Permite que você pesquise seu sistema e rede para o banco de dados ou o diretório para o qual você deseja se conectar à fonte de dados.  
  
 **Opções**  
 Expande a caixa de diálogo para que você pode definir opções de Driver de ODBC do Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequência de agrupamento**  
 A sequência na qual os campos são classificados. As sequências de padrão refletem as sequências de suporte para sua versão de idioma do sistema operacional. Para obter uma lista de sequências de agrupamento com suporte, consulte [definir COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando essa caixa de seleção é selecionada, o driver abre o banco de dados do Visual FoxPro exclusivamente ao acessar dados usando a fonte de dados. Outros usuários não podem acessar o banco de dados ou as tabelas no banco de dados enquanto o banco de dados é aberto exclusivamente. Tabelas no banco de dados aberto exclusivamente são abertas como compartilhado. Para abrir uma tabela de modo exclusivo, use o [definir exclusivo](../../odbc/microsoft/set-exclusive-command.md) comando. Essa caixa de seleção é desabilitada quando **tipo de banco de dados** é definido como **tabela livre**.  
  
 **NULL**  
 Determina se as colunas com ALTER TABLE e CREATE TABLE permitirão valores nulos. Se você definir ON nulo, inserir – SQL insere um valor nulo em qualquer coluna que não está incluída em uma instrução INSERT – SQL... Cláusula de valor. Um espaço em branco é inserido quando Null é OFF. Você também pode controlar essa opção por meio de uma cadeia de caracteres de conexão passada como o código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Excluído**  
 Determina se as linhas marcadas como excluídas são retornadas. Você também pode controlar essa opção por meio de uma cadeia de caracteres de conexão passada como o código a seguir:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Dados de busca em segundo plano**  
 Determina se os registros serão buscados em segundo plano (buscando progressivo) ou seu aplicativo aguardará até que todos os registros no conjunto de resultados.
