---
title: "Conceder direitos de administração de servidor a uma instância do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9caf9a17a4513c6261cad876ffb7aadce1c8ff09
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>Conceder direitos de administração de servidor a uma instância do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Membros da função de administrador de servidor em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] têm acesso irrestrito a todos os [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos e dados nessa instância. O usuário deve ser membro da função de administrador de servidor para realizar qualquer tarefa em todo o servidor, como criar ou processar um banco de dados, modificar propriedades do servidor ou iniciar um rastreamento (em vez de eventos de processamento).  
  
 A associação de função é estabelecida quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é instalado. O usuário que executa o programa de instalação pode adicionar a si mesmo à função ou adicionar outro usuário. Você deve especificar pelo menos um administrador antes que a instalação permita que você continue.  
  
 Por padrão, os membros do grupo Administradores local também recebem automaticamente direitos administrativos no Analysis Services. Embora o grupo local não seja explicitamente associado à função de administrador de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , os administradores locais podem criar bancos de dados, adicionar usuários e permissões, e executar qualquer outra tarefa permitida aos administradores do sistema. A concessão implícita de permissões de administrador é configurável. Ele é determinado pela propriedade de servidor **BuiltinAdminsAreServerAdmins** , que é definida como **true** por padrão. Você pode alterar essa propriedade em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Security Properties](../../analysis-services/server-properties/security-properties.md).  
  
 Após a instalação, você pode modificar a associação da função para adicionar quaisquer usuários que precisam de direitos totais para o serviço. Também é possível gerenciar funções de servidor com o Analysis Management Objects (AMO). Para obter mais informações, consulte [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Fornece uma progressão de funções cada vez mais granulares para processamento e consulta no servidor, banco de dados e níveis de objeto. Consulte [Funções e permissões &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md) para obter instruções sobre como usar essas funções.  
  
## <a name="modify-server-role-membership"></a>Modificar a associação a funções de servidor  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], clique com o botão direito do mouse no nome da instância no Pesquisador de Objetos e clique em **Propriedades**.  
  
2.  Clique em **Segurança** no painel **Selecionar uma Página** . Depois, clique em **Adicionar** na parte inferior da página para adicionar um ou mais usuários ou grupos do Windows à função de servidor.  
  
     ![Caixa de diálogo Adicionar usuários no management studio](../../analysis-services/instances/media/ssas-serveradminadd.png "caixa de diálogo Adicionar usuários no management studio")  
  
### <a name="add-computer-accounts"></a>Adicionar contas de computador  
 Você também pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para tornar uma conta de computador um membro do grupo de administradores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
1.  No diálogo **Selecionar Usuários ou Grupos** , clique em **Locais**.  
  
2.  Selecione o domínio do qual os computadores que você quer adicionar são membros ou selecione **Pasta inteira** e clique em **Ok**.  
  
3.  Clique em **Tipos de Objetos**.  
  
4.  Selecione **Computadores** e clique em **Ok**.  
  
     ![Adicionar contas de computador como administradores de ssas](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "adicionar contas de computador como administradores de ssas")  
  
5.  Na caixa de texto **Digite os nomes de objeto a serem selecionados** , digite o nome do computador e clique em **Verificar Nomes** para verificar se a conta do computador foi encontrada nos locais atuais. Se a conta de computador não for encontrada, verifique o nome do computador e o domínio correto do qual o computador é membro.  
  
## <a name="nt-servicessastelemetry-account"></a>Conta Serviço NT\SSASTelemetry  
 **Serviço NT/SSASTelemetry** é uma conta de computador com poucos privilégios criados durante a instalação e usada exclusivamente para executar a implementação de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do serviço CEIP (Programa de Aperfeiçoamento da Experiência do Usuário). Esse serviço requer direitos de administrador sobre a instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para executar vários comandos de identificação. Consulte [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) e [Microsoft SQL Server Privacy Statement](http://msdn.microsoft.com/library/57769f4a-5689-49a1-8298-e3c0db5106f8) para obter mais informações.  
  
## <a name="see-also"></a>Consulte Também  
 [Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Funções de Segurança &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
