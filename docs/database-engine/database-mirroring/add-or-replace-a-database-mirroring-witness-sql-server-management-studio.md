---
title: Adicionar ou substituir uma testemunha de espelho (SSMS)
description: Saiba como adicionar ou substituir uma testemunha de espelhamento de banco de dados usando o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- database mirroring [SQL Server], witness
ms.assetid: 4b5ecffd-f025-4ab7-b69d-8958c6477127
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 61e7be7b4e1f61f243d896d5073ae469bebe6940
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247502"
---
# <a name="add-or-replace-a-database-mirroring-witness-sql-server-management-studio"></a>Adicionar ou substituir uma testemunha de espelhamento de banco de dados (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se os pontos de extremidade do espelhamento de banco de dados usar Autenticação do Windows, você poderá usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para adicionar ou substituir uma testemunha. Ao adicionar uma testemunha ao [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] isso também altera o modo operacional para modo de segurança alta com failover automático.  
  
> [!NOTE]  
>  É altamente recomendável que a testemunha resida em um computador diferente do dos parceiros. A conta de serviço usada pela testemunha deve estar no mesmo domínio que as contas de serviço usadas pelas instâncias do servidor principal e espelho ou deve estar em um domínio confiável.  
  
### <a name="to-add-or-replace-a-witness"></a>Para adicionar ou substitui uma testemunha  
  
1.  Depois de se conectar à instância do servidor principal, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e selecione o banco de dados principal da sessão para a qual você está adicionando ou substituindo uma testemunha.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  Clique em **Configurar Segurança**.  
  
5.  Se a tela de boas-vindas do **Assistente para Configurar Segurança de Espelhamento de Banco de Dados** for exibida, clique em **Avançar**.  
  
6.  Na caixa de diálogo **Incluir Servidor Testemunha** , clique em **Sim**e, em seguida, clique em **Avançar**.  
  
7.  Na caixa de diálogo **Selecionar Servidores a Serem Configurados** , a caixa de seleção **Instância do servidor testemunha** é marcada automaticamente. Clique em **Próximo**.  
  
8.  Na caixa de diálogo **Instância do Servidor Principal** mantenha a porta e o ponto de extremidade existentes. Clique em **Próximo**.  
  
9. Na caixa de diálogo **Instância do Servidor Testemunha** , clique em **Conectar**.  
  
10. Na caixa de diálogo **Conectar ao Servidor** , especifique a instância de servidor testemunha no campo **Nome do servidor** e use Autenticação do Windows (o padrão). Clique em **Conectar**.  
  
11. Quando uma conexão é estabelecida, a porta do ouvinte e o ponto de extremidade do espelhamento de banco de dados da instância do servidor testemunha são exibidos na caixa de diálogo **Instância do Servidor Testemunha** . Clique em **Próximo**.  
  
12. A caixa de diálogo **Contas de Serviço** contém campos para as contas de serviço de domínio das instâncias de servidor principal, espelho e testemunha.  
  
    -   Se as instâncias de servidor usarem todas a mesma conta de serviço, deixe os campos em branco.  
  
    -   Se a instância do servidor testemunha usar uma conta de serviço diferente de qualquer um dos parceiros, preencha os campos **Principal**, **Espelho**e **Testemunha** com o nome de conta:  
  
         *DOMAINNAME* **\\** *username*  
  
         O nome de domínio deve estar em maiúscula.  
  
     Clique em **Próximo**.  
  
13. Opcionalmente, na tela de resumo **Concluir o Assistente** , verifique a configuração de testemunha e clique em **Concluir**.  
  
14. Ao terminar, o assistente o leva de volta para a caixa de diálogo **Propriedades do Banco de Dados** , em que agora o endereço de rede do servidor da testemunha aparece no campo **Testemunha** . Além disso, **High-safety mode with automatic failover (synchronous) (Modo de segurança alta com failover automático (síncrono))** , que é exigido com uma testemunha, é selecionado automaticamente.  
  
     Para habilitar a testemunha e alterar a sessão para o modo de segurança alta com failover automático, clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)   
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
