---
title: Referência de interface do usuário da caixa de diálogo funções do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- Package Roles dialog box
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ad91939638592cfbd1265bd77bff13b1d60b093a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019835"
---
# <a name="package-roles-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Funções do Pacote
  Use a caixa de diálogo **Funções do Pacote**, disponível no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para especificar as funções de nível de banco de dados que têm acesso de leitura e as que têm acesso de gravação ao pacote. As funções de nível de banco de dados se aplicam apenas a pacotes armazenados no banco de dados **msdbmsdb** do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para saber mais sobre as funções de nível de banco de dados do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e suas permissões, consulte [Funções do Integration Services &#40;Serviço SSIS&#41;](security/integration-services-roles-ssis-service.md).  
  
 As funções listadas na caixa de diálogo são as funções de banco de dados atuais do banco de dados de sistema **msdb** . Se nenhuma função for selecionada, serão aplicadas as funções do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Por padrão, a função de leitor inclui **db_ssisadmin**, **db_ssisoperator**e o usuário que criou o pacote. Um usuário membro de uma dessas funções ou criador dos pacotes pode enumerar, exibir, exportar e executar pacotes. Por padrão, a função de gravador inclui **db_ssisadmin** e o usuário que criou o pacote. Um usuário membro dessa função e o criador dos pacotes podem importar, excluir e alterar pacotes.  
  
 A coluna **ownersid** da tabela **sysssispackages** lista o identificador de segurança exclusivo do usuário que criou o pacote.  
  
## <a name="options"></a>Opções  
 **Nome do Pacote**  
 Especifique o nome do pacote.  
  
 **Função de Leitor**  
 Selecione uma função na lista.  
  
 **Função de Gravador**  
 Selecione uma função na lista  
  
## <a name="see-also"></a>Consulte também  
 [Funções de nível de banco de dados](../relational-databases/security/authentication-access/database-level-roles.md)   
 [Visão geral de segurança &#40;do Integration Services&#41;](security/security-overview-integration-services.md)  
  
  