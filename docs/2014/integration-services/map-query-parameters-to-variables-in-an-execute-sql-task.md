---
title: Mapear parâmetros de consulta para variáveis em uma tarefa Executar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 92972c340a71587329146f71542e15d8a45cb914
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233386"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>Mapear parâmetros de consulta para variáveis em uma tarefa Executar SQL
  Este tópico descreve como usar uma instrução SQL parametrizada na tarefa Executar SQL e criar mapeamentos entre variáveis e os parâmetros na instrução SQL.  
  
 Para saber mais sobre a tarefa Executar SQL, os marcadores de parâmetro e os nomes de parâmetro usados com diferentes tipos de conexão, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Para mapear um parâmetro de consulta para uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o qual você deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Se o pacote ainda não incluir uma tarefa Executar SQL, adicione uma ao fluxo de controle do pacote. Para obter mais informações, consulte [adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
5.  Clique duas vezes na tarefa Executar SQL.  
  
6.  Forneça um comando SQL parametrizado de um dos seguintes modos:  
  
    -   Use a entrada direta e digite o comando SQL na propriedade SQLStatement.  
  
    -   Use a entrada direta, clique em **Construir Consulta**e crie um comando SQL usando as ferramentas gráficas que o Construtor de Consultas fornece.  
  
    -   Use uma conexão de arquivo e depois faça referência ao arquivo que contém o comando SQL.  
  
    -   Use uma variável e depois faça referência à variável que contém o comando SQL.  
  
     Os marcadores de parâmetros que você usa nas instruções SQL parametrizadas dependem do tipo de conexão que a tarefa Executar SQL usa.  
  
    |Tipo de conexão|Marcador de parâmetro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET e SQLMOBILE|@\<nome do parâmetro>|  
    |ODBC|?|  
    |EXCEL e OLE DB|?|  
  
     A tabela a seguir lista exemplos do comando SELECT por tipo de gerenciador de conexões. Os parâmetros fornecem os valores de filtro nas cláusulas WHERE. Os exemplos usam SELECT para retornar produtos da tabela **Produto** em [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] que tenham uma **ProductID** maior e menor que os valores especificados pelos dois parâmetros.  
  
    |Tipo de conexão|Sintaxe de SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     Para obter exemplos de como usar parâmetros com procedimentos armazenados, consulte [Parameters and Return Codes in the Execute SQL Task](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
7.  Clique em **Mapeamento de Parâmetro**.  
  
8.  Para adicionar um mapeamento de parâmetro, clique em **Adicionar**.  
  
9. Forneça um nome na caixa **Nome do Parâmetro** .  
  
     Os nomes de parâmetros que você usa dependem do tipo de conexão que a tarefa Executar SQL usa.  
  
    |Tipo de conexão|Nome do Parâmetro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2,...|  
    |ADO.NET e SQLMOBILE|@\<nome do parâmetro>|  
    |ODBC|1, 2, 3, …|  
    |EXCEL e OLE DB|0, 1, 2, 3, …|  
  
10. Na lista **Nome da Variável** , selecione uma variável. Para obter mais informações, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
11. Na lista **Direção** , especifique se o parâmetro é uma entrada, uma saída ou um valor de retorno.  
  
12. Na lista **Tipo de Dados** , defina o tipo de dados do parâmetro.  
  
    > [!IMPORTANT]  
    >  O tipo de dados do parâmetro deve ser compatível com o tipo de dados da variável.  
  
13. Repita as etapas de 8 a 11 para cada parâmetro na instrução SQL.  
  
    > [!IMPORTANT]  
    >  A ordem dos mapeamentos de parâmetros deve ser igual à ordem em que os parâmetros aparecem na instrução SQL.  
  
14. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Executar SQL](control-flow/execute-sql-task.md)   
 [Parâmetros e códigos de retorno na tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Serviços de integração &#40;SSIS&#41; variáveis](integration-services-ssis-variables.md)  
  
  
