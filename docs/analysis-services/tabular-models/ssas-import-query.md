---
title: Importar dados usando uma consulta nativa (Analysis Services) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c313484b2ee7ff87668cbfdd0b87ed52cdaf98
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523968"
---
# <a name="import-data-by-using-a-native-query"></a>Importar dados usando uma consulta nativa
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
Para modelos de tabela 1400, a nova experiência obter dados em projetos do Visual Studio Analysis Services fornece enorme flexibilidade em como você pode realizar o mashup seus dados durante a importação. Este artigo descreve a criação de uma conexão a uma fonte de dados e, em seguida, criando uma consulta SQL nativa para especificar a importação de dados.

Para concluir as tarefas descritas neste artigo, verifique se que você estiver usando a versão mais recente do SSDT. Se você estiver usando o Visual Studio 2017, verifique se você baixou e instalou o setembro de 2017 ou posterior Microsoft Analysis Services projetos de VSIX.

[Baixar e instalar o SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Baixe o Microsoft Analysis Services projetos VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Criar uma conexão de fonte de dados
Se você ainda não tiver uma conexão para sua fonte de dados, você precisa criá-lo.

1. No Visual Studio > **Gerenciador de modelos tabulares**, clique com botão direito **fontes de dados**e, em seguida, clique em **nova fonte de dados**.
2. Na **obter dados**, selecione o tipo de fonte de dados e, em seguida, clique em **Connect**. Siga as etapas adicionais necessárias para se conectar à sua fonte de dados.


## <a name="enter-a-query-as-a-named-expression"></a>Insira uma consulta como uma expressão nomeada
1. Na **Gerenciador de modelos tabulares**, clique com botão direito **expressões** > **Editar expressões**.
2. Na **Editor de consultas**, clique em **consulta** > **nova consulta** > **consulta em branco**
3. Na barra de fórmulas, digite
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. Para criar uma tabela, no **consultas**, a consulta com o botão direito e, em seguida, selecione **criar nova tabela**. A nova tabela terá o mesmo nome que a consulta.


## <a name="example"></a>Exemplo
Esta consulta nativa cria uma tabela de funcionário no modelo que inclui todas as colunas da tabela Dimension.Employee na fonte de dados.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![Editor de consultas](media/ssas-import-query-example.png)


Após a importação, uma tabela denominada Employees é criada no modelo.   

![Editor de consultas](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>Confira também  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [Representação](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
