---
title: Fornecer uma consulta de OData Source em tempo de execução | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4dfabab76c036bc74e2085475d0c77e1500dac3f
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410708"
---
# <a name="provide-an-odata-source-query-at-runtime"></a>Fornecer uma consulta de OData Source em tempo de execução
 Você pode alterar a consulta de OData Source em tempo de execução adicionando uma *expressão* à propriedade **[Origem OData].[Consulta]** da Tarefa de Fluxo de Dados.  
  
 As colunas retornadas precisarão ser as mesmas colunas retornadas em tempo de design, caso contrário, você obterá um erro quando o pacote for executado. Certifique-se de especificar as mesmas colunas (na mesma ordem) ao usar a opção de consulta de $select. Uma alternativa mais segura para usar a opção de $select é desmarcar as colunas que você não deseja diretamente na interface de usuário do componente de origem.  
  
 Há algumas maneiras diferentes de definir dinamicamente o valor da consulta em tempo de execução. A seguir estão alguns dos métodos mais comuns.  
  
## <a name="provide-the-query-as-a-parameter"></a>Fornecer a consulta como um parâmetro  
 O procedimento a seguir mostra como expor a consulta usada por um componente de OData Source como um parâmetro do pacote.  
  
1.  Clique com o botão direito do mouse em **Tarefa de Fluxo de Dados** e selecione a opção **Parametrizar...** .  
  
2.  No diálogo **Parametrizar**, selecione **[\<Nome do Componente de OData Source].[Consulta]** para **Propriedade**.  
  
3.  Escolha se deseja **criar novo parâmetro** ou **usar um parâmetro existente**.  
  
4.  Se você selecionar **Criar novo parâmetro**:  
  
    1.  Insira um **nome** e **descrição** para o parâmetro.  
  
    2.  Especifique o **valor** padrão para o parâmetro.  
  
    3.  Especifique o **escopo** (**pacote** ou **projeto**) para o parâmetro.  
  
    4.  Especifique se o parâmetro é ou não **obrigatório**  
  
5.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="provide-the-query-with-an-expression"></a>Forneça a consulta com uma expressão
 Este método será útil quando você desejar construir dinamicamente a cadeia de consulta em tempo de execução.
  
1.  Selecione a **Tarefa de Fluxo de Dados** que contém o **OData Source**.  
  
2.  Na janela **Propriedades** , destaque a propriedade **Expressões** .  
  
3.  Clique no botão ... (reticências) para abrir o **Editor de Expressões de Propriedade**.  
  
4.  Selecione a propriedade de **[Fonte do OData].[Consulta]** .  
  
5.  Clique no botão ... (reticências) da **Expressão**.  
  
6.  Insira a **expressão**.  
  
7.  Clique em **OK**.  
  
> [!NOTE]  
> Observe que, ao usar essa abordagem, você precisa garantir que os valores definidos estejam adequadamente em formato codificado de URL. Ao receber valores de entrada do usuário (por exemplo, definindo valores de opção consulta individual de um parâmetro), certifique-se de que os valores sejam validados para impedir ataques potenciais do tipo injeção do SQL.  
  
  
