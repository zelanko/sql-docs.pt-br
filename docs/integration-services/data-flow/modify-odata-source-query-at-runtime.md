---
title: "Fornecer uma consulta de origem OData em tempo de execução | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: pt-br
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>Fornecer uma consulta de origem OData em tempo de execução
 Você pode modificar a consulta de origem OData em tempo de execução, adicionando um *expressão* para o **[OData Source]. [ Consulta]** propriedade da tarefa de fluxo de dados.  
  
 As colunas retornadas precisam ser as mesmas colunas que foram retornadas em tempo de design; Caso contrário, você obterá um erro quando o pacote é executado. Certifique-se de especificar as mesmas colunas (na mesma ordem) ao usar a opção de consulta de $select. Uma alternativa mais segura para usar a opção de $select é desmarcar as colunas que você não deseja diretamente na interface de usuário do componente de origem.  
  
 Há algumas maneiras diferentes de definir dinamicamente o valor da consulta em tempo de execução. Aqui estão alguns dos métodos mais comuns.  
  
## <a name="provide-the-query-as-a-parameter"></a>Forneça a consulta como um parâmetro  
 O procedimento a seguir mostra como expor a consulta usada por um componente de origem OData como um parâmetro do pacote.  
  
1.  Clique com o botão direito do mouse em **Tarefa de Fluxo de Dados** e selecione a opção **Parametrizar...** .  
  
2.  No **parametrizar** caixa de diálogo, selecione **[\<nome do componente de origem OData >]. [ Consulta]** para **propriedade**.  
  
3.  Escolha se deseja **criar novo parâmetro** ou **usar um parâmetro existente**.  
  
4.  Se você selecionar **criar novo parâmetro**:  
  
    1.  Insira um **nome** e **descrição** para o parâmetro.  
  
    2.  Especifique o **valor** padrão para o parâmetro.  
  
    3.  Especifique o **escopo** (**pacote** ou **projeto**) para o parâmetro.  
  
    4.  Especifique se o parâmetro é ou não **obrigatório**  
  
5.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="provide-the-query-with-an-expression"></a>Forneça a consulta com uma expressão
 Esse método é útil quando você deseja construir dinamicamente a cadeia de caracteres de consulta em tempo de execução.
  
1.  Selecione o **a tarefa de fluxo de dados** que contém seu **fonte OData**.  
  
2.  Na janela **Propriedades** , destaque a propriedade **Expressões** .  
  
3.  Clique no botão (reticências) para exibir o **Editor de expressões de propriedade**.  
  
4.  Selecione a propriedade de **[Fonte do OData].[Consulta]** .  
  
5.  Clique no botão de (reticências) **expressão**.  
  
6.  Insira a **expressão**.  
  
7.  Clique em **OK**.  
  
> [!NOTE]  
> Quando você usar essa abordagem, você precisa garantir que os valores definidos corretamente são codificados de URL. Ao receber valores de entrada do usuário (por exemplo, definindo valores de opção consulta individual de um parâmetro), certifique-se de que os valores sejam validados para impedir ataques potenciais do tipo injeção do SQL.  
  
  

