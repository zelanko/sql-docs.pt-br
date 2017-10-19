---
title: Importar dados usando uma consulta nativa (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 10/02/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 8888951d9fca0013015105998200b3ee9364855d
ms.contentlocale: pt-br
ms.lasthandoff: 10/11/2017

---
# <a name="import-data-by-using-a-native-query"></a>Importar dados usando uma consulta nativa

1400 para modelos de tabela, a nova experiência de obter dados em projetos do Visual Studio Analysis Services fornece enorme flexibilidade em como você pode mashup seus dados durante a importação. Este artigo descreve a criação de uma conexão a uma fonte de dados e, em seguida, criar uma consulta SQL nativa para especificar a importação de dados.

Para concluir as tarefas descritas neste artigo, verifique se que você estiver usando a versão mais recente do SSDT. Se você estiver usando o Visual Studio de 2017, verifique se você baixou e instalou o de 2017 setembro ou posterior VSIX de projetos Microsoft Analysis Services.

[Baixar e instalar o SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Baixar o Microsoft Analysis Services projetos VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Criar uma conexão de fonte de dados
Se você ainda não tiver uma conexão à sua fonte de dados, você precisa criar um.

1. No Visual Studio > **Gerenciador de modelos tabulares**, clique com botão direito **fontes de dados**e, em seguida, clique em **nova fonte de dados**.
2. Em **obter dados**, selecione o tipo de fonte de dados e, em seguida, clique em **conectar**. Siga as etapas adicionais necessárias para se conectar à sua fonte de dados.


## <a name="enter-a-query-as-a-named-expression"></a>Insira uma consulta como uma expressão nomeada
1. Em **Gerenciador de modelos tabulares**, clique com botão direito **expressões** > **Editar expressões**.
2. Em **Editor de consultas**, clique em **consulta** > **nova consulta** > **consulta em branco**
3. Na barra de fórmulas, digite
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM …")
    ```
4. Para criar uma tabela no **consultas**, a consulta e, em seguida, selecione **criar nova tabela**. A nova tabela terá o mesmo nome que a consulta.


## <a name="example"></a>Exemplo
Essa consulta nativa cria uma tabela de funcionários no modelo que inclui todas as colunas da tabela Dimension.Employee na fonte de dados.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![Editor de consultas](media/ssas-import-query-example.png)


Após a importação, uma tabela chamada funcionários é criada no modelo.   

![Editor de consultas](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>Consulte também  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [Representação](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  

