---
title: Modificar consulta de origem OData em tempo de execução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2c355c95c5e6c686a063c4c32081aa0740f8e2fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915206"
---
# <a name="modify-odata-source-query-at-runtime"></a>Modifique a consulta de origem do OData em runtime
  Você pode alterar a consulta de origem OData em runtime adicionando uma expressão à propriedade de **[OData Source].[Consulta]** da Tarefa de Fluxo de Dados.  
  
 Observe que as colunas devem permanecer iguais às que foram usadas em tempo de design; caso contrário, você receberá um erro quando o pacote for executado. Certifique-se de especificar as mesmas colunas (na mesma ordem) ao usar a opção de consulta de $select. Uma alternativa mais segura para usar a opção de $select é desmarcar as colunas que você não deseja diretamente na interface do usuário do componente de origem.  
  
 Há algumas maneiras diferentes de definir dinamicamente o valor da consulta em runtime. A seguir estão alguns dos métodos mais comuns.  
  
## <a name="exposing-the-query-as-a-parameter"></a>Expor a consulta como um parâmetro  
 O procedimento a seguir tem etapas para expor a consulta usada por um componente de origem OData como um parâmetro ao pacote.  
  
1.  Clique com o botão direito do mouse em **Tarefa de Fluxo de Dados** e selecione a opção **Parametrizar...** .  
  
2.  Na caixa de diálogo **parametrizar** , selecione **[ \<Name of the OData Source Component> ]. [ Query]** para **Propriedade**.  
  
3.  Escolha se deseja **criar novo parâmetro** ou **usar um parâmetro existente**.  
  
4.  Se você selecionar **Criar novo parâmetro**, faça o seguinte:  
  
    1.  Insira um **nome** e **descrição** para o parâmetro.  
  
    2.  Especifique o **valor** padrão para o parâmetro.  
  
    3.  Especifique o **escopo** (**pacote** ou **projeto**) para o parâmetro.  
  
    4.  Especifique se o parâmetro é ou não **obrigatório**  
  
5.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="using-an-expression"></a>Usando uma expressão  
 Este método será útil quando você desejar construir dinamicamente a cadeia de caracteres de consulta em runtime. Neste exemplo, a variável MaxRows será definida com outros meios (script, parâmetro, etc.).  
  
1.  Selecione a **Tarefa de Fluxo de Dados** que contém a sua **Fonte OData**.  
  
2.  Na janela **Propriedades** , destaque a propriedade **Expressões** .  
  
3.  Clique em... botão (reticências) para abrir o **Editor de expressões de propriedade**.  
  
4.  Selecione a propriedade de **[Fonte do OData].[Consulta]** .  
  
5.  Clique em... botão (reticências) da **expressão**.  
  
6.  Insira a **expressão**.  
  
7.  Clique em **OK**.  
  
> [!WARNING]  
>  Observe que ao usar essa abordagem você precisa garantir que os valores definidos sejam codificados corretamente no URL. Ao receber valores de entrada do usuário (por exemplo, definindo valores de opção consulta individual de um parâmetro), certifique-se de que os valores sejam validados para impedir ataques potenciais do tipo injeção do SQL.  
  
  
