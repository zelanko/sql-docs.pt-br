---
title: 'Tarefa 4: definindo regras de domínio | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd59bf315e90bd52ba1388d27c533ab4a3136d3c
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381738"
---
# <a name="task-4-setting-domain-rules"></a>Tarefa 4: Definindo regras de domínio
  Nesta tarefa, você cria uma regra para o domínio de **email de contato** para verificar se o endereço de email termina com **\@adventure-Works.com**. Consulte o tópico [criando uma regra de domínio](https://msdn.microsoft.com/library/hh510397.aspx) para obter mais detalhes sobre a página.  
  
1.  Clique em **email de contato** na lista de **domínios**.  
  
2.  Alterne para a guia **regras de domínio** no painel direito.  
  
     ![Botão da barra de ferramentas adicionar um novo domínio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "Botão da barra de ferramentas adicionar um novo domínio")  
  
3.  No painel direito, clique no botão **Adicionar uma nova regra de domínio** na barra de ferramentas (consulte a imagem) para adicionar uma regra.  
  
4.  Digite **validação de email** para o **nome da regra** e pressione **Enter**. A caixa de seleção **ativa** deve ser marcada por padrão. Esse controle permite a você desativar temporariamente uma regra.  
  
5.  No painel **criar uma regra** , clique na **seta para baixo**e selecione **valor termina com**.  
  
6.  Digite **\@adventure-Works.com** na caixa de texto e pressione **Tab**. Você pode adicionar mais condições clicando em **Adicionar uma nova condição ao** botão da barra de ferramentas da cláusula selecionada no painel **criar uma regra** .  
  
     ![Regra de validação de email](../../2014/tutorials/media/et-settingdomainrules-02.jpg "Regra de validação de email")  
  
7.  Clique no botão **executar a regra de domínio selecionada no dados de teste** na barra de ferramentas no painel direito para testar a regra em relação aos dados de exemplo.  
  
     ![Executar a regra de domínio no botão da barra de ferramentas dados de teste](../../2014/tutorials/media/et-settingdomainrules-03.jpg "Executar a regra de domínio no botão da barra de ferramentas dados de teste")  
  
8.  Na caixa de diálogo **testar regra de domínio** , clique em **adiciona um novo termo de teste para o botão regra de domínio** na barra de ferramentas.  
  
     ![Caixa de diálogo testar regra de domínio](../../2014/tutorials/media/et-settingdomainrules-04.jpg "Caixa de diálogo testar regra de domínio")  
  
9. Digite **frank7\@adventure-works.com** (um valor válido) na coluna **email de contato** .  
  
10. Repita as duas etapas anteriores para adicionar **joe2\@adventure-work.com** (um valor inválido sem ' ').  
  
11. Clique no botão último (**teste a regra de domínio em todos os termos**) na barra de ferramentas para testar os dados de entrada em relação à regra.  
  
     ![Botão de barra de ferramentas testar regra de domínio em todos os termos](../../2014/tutorials/media/et-settingdomainrules-05.jpg "Botão de barra de ferramentas testar regra de domínio em todos os termos")  
  
12. Observe que a primeira entrada será mostrada como um item válido e a segunda como um item inválido.  
  
     ![Testar resultados da regra de domínio](../../2014/tutorials/media/et-settingdomainrules-06.jpg "Testar resultados da regra de domínio")  
  
13. Clique em **fechar** para fechar a caixa de diálogo **testar regra de domínio** .  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Definindo relações baseadas em termos](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
