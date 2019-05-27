---
title: Configuração do mecanismo - instância de usuário de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095876"
---
# <a name="database-engine-configuration---user-instance"></a>Configuração do Mecanismo de Banco de Dados - Instância de usuário
  Use a página **Instância de Usuário** para gerar uma instância separada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usuários sem permissões de administrador e adicione usuários à função de administrador.  
  
## <a name="option"></a>Opção  
 Habilitar instâncias de usuário  
 O padrão é habilitado. Para desabilitar a funcionalidade de habilitar instâncias de usuário, desmarque a caixa de seleção.  
  
 A instância do usuário, também conhecida como instância filha ou cliente, é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerada pela instância pai (a instância primária executada como um serviço, como o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) em nome de um usuário. A instância de usuário é executada como um processo de usuário no contexto de segurança daquele usuário. A instância de usuário é isolada da instância pai e de qualquer outra instância de usuário que estiver em execução no computador. O recurso de instância de usuário também é chamado de RANU "Run As Normal User" (Executar como Usuário Normal).  
  
> [!NOTE]  
>  Logons provisionados como membros da função de servidor fixa **sysadmin** durante a instalação são provisionados como administradores no banco de dados de modelo. Eles são membros da função de servidor fixa **sysadmin** na instância de usuário, a menos que sejam removidos  
  
 Adicionar usuário à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O padrão é desabilitado. Para adicionar o usuário de instalação atual à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , marque a caixa de seleção.  
  
 Usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] que são membros de BUILTIN\Administrators não são adicionados automaticamente à função de servidor fixa sysadmin quando se conectam a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Somente os usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] explicitamente adicionados a uma função de administrador de nível de servidor podem administrar o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Qualquer membro do grupo Built-In\Users pode se conectar à instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , mas terá permissões limitadas para executar tarefas do banco de dados. Por esse motivo, os usuários cujos privilégios do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] sejam herdados de BUILTIN\Administradores e Built-In\Users das versões anteriores do Windows devem receber explicitamente privilégios administrativos em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] executadas no [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Para fazer qualquer alteração nas funções de usuário após a conclusão deste programa de instalação, use a ferramenta SQLSAC.exe (Configuração da Área de Superfície) do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para atualizar a lista de usuários na função de Administrador de Sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Adicionar Novo Administrador** .  
  
 Verifique se o campo **Usuário para provisionamento** lista o NomeDeDomínio\NomeDeUsuário do usuário cujas permissões devem ser atualizadas. Selecione a função que será atualizada na lista de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no painel **Privilégios disponíveis** e clique na seta à direita. Para adicionar o usuário a todas as funções para todas as instâncias disponíveis das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todas as funções disponíveis, clique duas vezes na seta à direita.  
  
 Para implementar as alterações quando suas seleções estiverem completas, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. Para encerrar o uso da ferramenta sem fazer alterações, clique em **Cancelar**.  
  
  
