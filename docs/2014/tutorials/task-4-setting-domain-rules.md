---
title: 'Tarefa 4: Definindo regras de domínio | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 89e0027b3bf1748fb68a8b6922c45572a7b41bb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011921"
---
# <a name="task-4-setting-domain-rules"></a>Tarefa 4: Definindo regras de domínio
  Nesta tarefa, você pode criar uma regra para o **Contact Email** domínio para verificar se o endereço de email termina com **@adventure-works.com**. Consulte [criar uma regra de domínio](http://msdn.microsoft.com/library/hh510397.aspx) tópico para obter mais detalhes sobre a página.  
  
1.  Clique em **Contact Email** no **lista de domínios**.  
  
2.  Alterne para o **regras de domínio** guia no painel direito.  
  
     ![Adicionar um novo botão de barra de ferramentas de regra de domínio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "adicionar um novo botão de barra de ferramentas de regra de domínio")  
  
3.  No painel direito, clique em **adicionar uma nova regra de domínio** na barra de ferramentas (consulte a imagem) para adicionar uma regra.  
  
4.  Tipo **validação de Email** para o **o nome da regra** e pressione **ENTER**. O **Active** caixa de seleção deverá ser marcada por padrão. Esse controle permite a você desativar temporariamente uma regra.  
  
5.  No **criar uma regra** painel, clique em **a seta para baixo**e selecione **valor termina com**.  
  
6.  Tipo **@adventure-works.com** na caixa de texto e pressione **guia**. Você pode adicionar mais condições clicando **adicionar uma nova condição à cláusula selecionada** botão da barra de ferramentas no **criar uma regra** painel.  
  
     ![Regra de validação de email](../../2014/tutorials/media/et-settingdomainrules-02.jpg "regra de validação de Email")  
  
7.  Clique em **executar a regra de domínio selecionada em dados de teste** na barra de ferramentas no painel direito para testar a regra em relação aos dados de exemplo.  
  
     ![Executar a regra de domínio em botão de barra de ferramentas de dados de teste](../../2014/tutorials/media/et-settingdomainrules-03.jpg "executar a regra de domínio em botão de barra de ferramentas de dados de teste")  
  
8.  No **testar regra de domínio** caixa de diálogo, clique em **adiciona um novo termo de teste para a regra de domínio** na barra de ferramentas.  
  
     ![Caixa de diálogo de regra de domínio de teste](../../2014/tutorials/media/et-settingdomainrules-04.jpg "testar caixa de diálogo de regra de domínio")  
  
9. Tipo **frank7@adventure-works.com** (um valor válido) no **Contact Email** coluna.  
  
10. Repita as duas etapas anteriores para adicionar **joe2@adventure-work.com** (um valor inválido sem do ').  
  
11. Clique no botão última (**teste a regra de domínio em todos os termos**) na barra de ferramentas para testar os dados de entrada em relação à regra.  
  
     ![Testar a regra de domínio em todos os botões de barra de ferramentas de termos](../../2014/tutorials/media/et-settingdomainrules-05.jpg "testar a regra de domínio em todos os botões de barra de ferramentas de termos")  
  
12. Observe que a primeira entrada será mostrada como um item válido e a segunda como um item inválido.  
  
     ![Testar os resultados da regra de domínio](../../2014/tutorials/media/et-settingdomainrules-06.jpg "resultados de regra de domínio de teste")  
  
13. Clique em **fechar** para fechar o **testar regra de domínio** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Definindo relações baseadas em termos](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  