---
title: Caixa de diálogo de configuração Visual FoxPro da ODBC | Microsoft Docs
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
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298076"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Caixa de diálogo da instalação do Visual FoxPro do ODBC
A caixa de diálogo **Configuração Visual FoxPro do ODBC** permite adicionar ou alterar uma fonte de dados Visual FoxPro.  
  
 Para baixar o driver, consulte [o site de download visual FoxPro ODBC Driver](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opções de caixa de diálogo  
 **Nome da fonte de dados**  
 Digite o nome que deseja usar para a fonte de dados.  
  
 **Descrição**  
 Digite uma descrição para a fonte de dados.  
  
 **Tipo de banco de dados**  
 Permite que você escolha o tipo de banco de dados ao qual deseja que sua fonte de dados se conecte.  
  
 **Banco de dados Visual FoxPro (. DBC)**  
 Especifica que a fonte de dados se conecta a um [banco de dados](../../odbc/microsoft/visual-foxpro-terminology.md) Visual FoxPro (arquivo.dbc) e a todas as tabelas e visualizações locais no banco de dados.  
  
 **Diretório de Mesa Livre**  
 Especifica que a fonte de dados se conecta a um diretório de [tabelas gratuitas](../../odbc/microsoft/visual-foxpro-terminology.md). Quaisquer tabelas de banco de [dados](../../odbc/microsoft/visual-foxpro-terminology.md) no mesmo diretório são ignoradas pelas funções do catálogo ODBC, como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ou [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). As tabelas de banco de dados podem ser acessadas usando instruções SQL SELECT enviadas através [do SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [do SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Caminho**  
 Exibe o caminho e o nome do banco de dados ou do diretório de tabelas gratuitas às quais a fonte de dados se conecta.  
  
 **Procurar**  
 Permite que você pesquise seu sistema e rede para o banco de dados ou diretório ao qual deseja conectar a fonte de dados.  
  
 **Opções**  
 Expande a caixa de diálogo para que você possa definir as opções de driver Visual FoxPro ODBC.  
  
## <a name="driver"></a>Driver  
 **Sequência de colisão**  
 A seqüência em que os campos são classificados. As seqüências padrão refletem as seqüências suportadas pela versão de idioma do sistema operacional. Para obter uma lista de seqüências de colagem suportadas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando esta caixa de seleção é selecionada, o driver abre o banco de dados Visual FoxPro exclusivamente quando você acessa dados usando a fonte de dados. Outros usuários não podem acessar o banco de dados ou as tabelas no banco de dados enquanto o banco de dados é aberto exclusivamente. As tabelas dentro do banco de dados exclusivamente aberto são abertas como COMPARTILHADAs. Para abrir uma tabela exclusivamente, use o comando [SET EXCLUSIVE.](../../odbc/microsoft/set-exclusive-command.md) Esta caixa de seleção é desativada quando **o tipo de banco de dados** é definido como diretório de tabela **livre**.  
  
 **Null**  
 Determina se as colunas criadas com TABELA ALTER e TABELA CRIAR permitem valores nulos. Se você definir Null ON, INSERT - SQL insere um valor nulo em qualquer coluna não incluída em um INSERT - SQL... Cláusula DE VALOR. Um branco é inserido se Nulo estiver DESLIGADO. Você também pode controlar essa opção através de uma seqüência de conexões passadas como no seguinte código:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Excluído**  
 Determina se as linhas marcadas como excluídas são devolvidas. Você também pode controlar essa opção através de uma seqüência de conexões passadas como no seguinte código:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Buscar dados em segundo plano**  
 Determina se os registros serão obtidos em segundo plano (busca progressiva) ou se sua aplicação aguardará até que todos os registros no conjunto de resultados sejam buscados.
