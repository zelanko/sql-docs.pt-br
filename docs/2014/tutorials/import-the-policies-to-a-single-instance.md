---
title: Importar as políticas para uma única instância | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 410f3a317a9d3ad2f8cab52d9f57fd4a63c1c36c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014137"
---
# <a name="import-the-policies-to-a-single-instance"></a>Importar as políticas para uma única instância
  Nesta tarefa, você importará as políticas de práticas recomendadas que deseja agendar no Gerenciamento Baseado em Políticas em uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Você deve executar este procedimento em um servidor que está executando o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ou uma versão posterior.  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>Importar as políticas de práticas recomendadas para o Mecanismo de Banco de Dados  
  
1.  Inicie o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]e conecte-se ao [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  No Pesquisador de Objetos, expanda **Gerenciamento**e, em seguida, expanda **Gerenciamento de Políticas**.  
  
3.  Clique com o botão direito do mouse em **Políticas**e clique em **Importar Política**.  
  
4.  No **importação** caixa de diálogo, em seguida o **arquivos a importar** , clique no botão de reticências (**...** ) botão.  
  
5.  Na lista **Examinar** , navegue até a pasta a seguir, que contém as políticas de práticas recomendadas:  
  
     **C:\Program arquivos (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  O caminho do arquivo pode variar, dependendo de onde você instalou os arquivos de programa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , do sistema operacional em execução (32 bits ou 64 bits) e do identificador de idioma.  
  
6.  Na caixa de diálogo **Selecionar Política** , selecione um ou mais arquivos de política.  
  
     Para selecionar arquivos não adjacentes, clique em um arquivo, mantenha a tecla CTRL pressionada e clique em cada arquivo adicional. Para selecionar arquivos adjacentes, clique no primeiro arquivo da sequência, mantenha a tecla SHIFT pressionada e clique no último arquivo.  
  
7.  Após terminar de selecionar os arquivos, clique em **Abrir**.  
  
8.  Na caixa de diálogo **Importar** , verifique se a lista **Estado da política** está definida como **Preservar o estado da política ao importar** (o padrão) e, em seguida, clique em **OK**.  
  
     As políticas são importadas no nó **Políticas** em **Gerenciamento de Políticas**. Por padrão, as políticas importadas são definidas como modo de avaliação "Sob demanda."  
  
## <a name="next-steps"></a>Próximas etapas  
 [Agendar as políticas](../../2014/tutorials/schedule-the-policies.md)  
  
  
