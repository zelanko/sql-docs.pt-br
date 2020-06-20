---
title: 'Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dd1727ffaa24edf12ed7ad8a5fb4f55f4910855e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064816"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência
  Nesta tarefa, você configura o domínio composto de **validação de endereço** para usar o serviço de verificação de **endereço de dados Melissa** . Em runtime, durante a atividade de limpeza, o DQS passa os valores de domínios existentes no domínio Address Validation para o serviço de limpeza. Consulte [mapear domínio/domínio de composição para dados de referência](https://msdn.microsoft.com/library/hh213030.aspx) para obter mais detalhes.  
  
1.  Na página principal do **cliente do DQS**, clique em **fornecedores (gerenciamento de domínio)** em **bases de dados de conhecimento recentes** para iniciar a página de **Gerenciamento de domínio** .  
  
2.  Selecione o domínio composto **validação de endereço** na **lista de domínios**.  
  
3.  No painel direito, alterne para a guia **dados de referência** .  
  
     ![Guia Dados de Referência](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "Guia Dados de Referência")  
  
4.  Clique no botão **procurar** na barra de ferramentas.  
  
5.  Na caixa de diálogo **Catálogo de provedores de dados de referência online** , marque a **caixa de seleção** ao lado de **Melissa verificação de endereço de dados**.  
  
     ![Selecionar Melissa Data - Verificação de Endereço](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Selecionar Melissa Data - Verificação de Endereço")  
  
6.  No painel direito, na seção **esquema** , mapeie o domínio da **linha de endereço** para o item de esquema da linha de **Endereço (M)** usando a lista suspensa.  
  
     ![Mapear Item de Esquema do RDS para Domínio](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "Mapear Item de Esquema do RDS para Domínio")  
  
7.  Clique no botão **Adicionar entrada de esquema (+)** na barra de ferramentas para criar uma entrada na lista.  
  
     ![Botão de barra de ferramentas Adicionar Entrada de Esquema](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "Botão de barra de ferramentas Adicionar Entrada de Esquema")  
  
8.  Mapeie os seguintes domínios do DQS usando as listas suspensas como mostra a imagem a seguir.  
  
     ![Mapear Itens de Esquema do RDS para Domínios](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "Mapear Itens de Esquema do RDS para Domínios")  
  
9. Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 11: Publicando a base de dados de conhecimento](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
