---
title: 'Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a5d37578ac8336b67201161ef4de59baf90649c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010569"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência
  Nesta tarefa, você deve configurar o **Address Validation** domínio composto para usar o **Melissa Data – Address Check** serviço. Em tempo de execução, durante a atividade de limpeza, o DQS passa os valores de domínios existentes no domínio Address Validation para o serviço de limpeza. Consulte [mapear domínio/domínio composto para dados de referência](http://msdn.microsoft.com/library/hh213030.aspx) para obter mais detalhes.  
  
1.  Na página principal do **cliente DQS**, clique em **fornecedores (gerenciamento de domínio)** em **Bases de conhecimento recente** para iniciar o **gerenciamento de domínio**página.  
  
2.  Selecione o **Address Validation** domínio composto no **lista de domínios**.  
  
3.  No painel direito, alterne para o **dados de referência** guia.  
  
     ![Guia dados de referência](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "guia dados de referência")  
  
4.  Clique em **procurar** na barra de ferramentas.  
  
5.  Sobre o **catálogo de provedores de dados de referência Online** caixa de diálogo, selecione **caixa de seleção** lado **Melissa Data – Address Check**.  
  
     ![Selecionar Melissa Data - verificação de endereço](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "selecionar Melissa Data - verificação de endereço")  
  
6.  No painel direito, no **esquema** seção, mapeie **Address Line** domínio para o **Address Line (M)** item do esquema usando a lista suspensa.  
  
     ![Mapear Item de esquema do RDS para domínio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "mapear Item de esquema do RDS para domínio")  
  
7.  Clique em **Adicionar entrada de esquema (+)** na barra de ferramentas para criar uma entrada na lista.  
  
     ![Adicionar um botão de barra de ferramentas de entrada de esquema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "adicionar um botão de barra de ferramentas de entrada de esquema")  
  
8.  Mapeie os seguintes domínios do DQS usando as listas suspensas como mostra a imagem a seguir.  
  
     ![Mapear itens de esquema do RDS para domínios](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "mapear itens de esquema do RDS para domínios")  
  
9. Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 11: Publicando a base de dados de conhecimento](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  