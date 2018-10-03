---
title: 'Tarefa 4: Definindo regras de domínio | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3c8bbc2bb88747aee84be9eeff18fcae59df54d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138722"
---
# <a name="task-4-setting-domain-rules"></a>Tarefa 4: Definindo regras de domínio
  Nesta tarefa, você pode criar uma regra para o **Contact Email** domínio para verificar se o endereço de email termina com **@adventure-works.com**. Ver [criando uma regra de domínio](http://msdn.microsoft.com/library/hh510397.aspx) tópico para obter mais detalhes sobre a página.  
  
1.  Clique em **Contact Email** na **lista de domínios**.  
  
2.  Alterne para o **regras de domínio** guia no painel à direita.  
  
     ![Adicionar um novo botão de barra de ferramentas de regra de domínio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "adicionar um novo botão de barra de ferramentas de regra de domínio")  
  
3.  No painel direito, clique em **adicionar uma nova regra de domínio** na barra de ferramentas (consulte a imagem) para adicionar uma regra.  
  
4.  Tipo de **validação de Email** para o **nome da regra** e pressione **ENTER**. O **Active** caixa de seleção deve ser marcada por padrão. Esse controle permite a você desativar temporariamente uma regra.  
  
5.  No **uma regra de compilação** painel, clique em **seta para baixo**e selecione **valor termina com**.  
  
6.  Tipo de **@adventure-works.com** na caixa de texto e pressione **guia**. Você pode adicionar mais condições clicando **adicionar uma nova condição à cláusula selecionada** botão de barra de ferramentas na **criar uma regra** painel.  
  
     ![Regra de validação de email](../../2014/tutorials/media/et-settingdomainrules-02.jpg "regra de validação de Email")  
  
7.  Clique em **executar a regra de domínio selecionada em dados de teste** na barra de ferramentas no painel direito para testar a regra em relação aos dados de exemplo.  
  
     ![Executar a regra de domínio em botão de barra de ferramentas de dados de teste](../../2014/tutorials/media/et-settingdomainrules-03.jpg "executar a regra de domínio em botão de barra de ferramentas de dados de teste")  
  
8.  No **testar regra de domínio** caixa de diálogo, clique em **adiciona um novo termo de teste para a regra de domínio** na barra de ferramentas.  
  
     ![Testar caixa de diálogo de regra de domínio](../../2014/tutorials/media/et-settingdomainrules-04.jpg "testar caixa de diálogo de regra de domínio")  
  
9. Tipo de **frank7@adventure-works.com** (um valor válido) na **Contact Email** coluna.  
  
10. Repita as duas etapas anteriores para adicionar **joe2@adventure-work.com** (um valor inválido sem do ').  
  
11. Clique no botão última (**teste a regra de domínio em todos os termos**) na barra de ferramentas para testar os dados de entrada em relação à regra.  
  
     ![Testar a regra de domínio em botão de barra de ferramentas de todos os termos](../../2014/tutorials/media/et-settingdomainrules-05.jpg "a regra de domínio em botão de barra de ferramentas de todos os termos de teste")  
  
12. Observe que a primeira entrada será mostrada como um item válido e a segunda como um item inválido.  
  
     ![Resultados da regra de domínio de teste](../../2014/tutorials/media/et-settingdomainrules-06.jpg "resultados da regra de domínio de teste")  
  
13. Clique em **feche** para fechar o **testar regra de domínio** caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 5: Definindo relações baseadas em termos](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
