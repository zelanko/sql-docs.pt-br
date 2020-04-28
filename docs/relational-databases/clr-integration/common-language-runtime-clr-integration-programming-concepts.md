---
title: Programação CLR (Common Language Runtime)
description: Este artigo fornece recursos para usar a integração CLR com o SQL Server, que permite que você grave módulos do lado do servidor usando qualquer linguagem de .NET Framework.
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- CLR [SQL Server] See common language runtime [SQL Server]
- Database Engine [SQL Server], .NET Framework
- .NET Framework [SQL Server], Database Engine programming
- common language runtime [SQL Server]
- .NET Framework [SQL Server]
ms.assetid: 951bf851-3e6e-4361-ae6a-2bcd5b837ebd
author: rothja
ms.author: jroth
ms.openlocfilehash: c44e777e78e9d2a6ded97e5bff2ec61e4c7f8391
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488100"
---
# <a name="common-language-runtime-clr-integration-programming-concepts"></a>Conceitos de programação da Integração CLR (Common Language Runtime)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresenta a integração do componente CLR do .NET Framework para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Isso significa que você pode agora gravar procedimentos armazenados, gatilhos, tipos definidos pelo usuário, funções definidas pelo usuário, agregações definidas pelo usuário e funções de streaming com valor de tabela, usando qualquer linguagem do .NET Framework, incluindo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 O namespace Microsoft.SqlServer.Server inclui a funcionalidade principal para programação de CLR no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, o namespace Microsoft.SqlServer.Server é documentado no .NET Framework SDK. Esta documentação não é incluída em Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Por padrão, o .NET Framework é instalado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não o .NET Framework SDK. Sem o SDK instalado no computador e incluído na coleção de Manuais Online, os links para o conteúdo do SDK desta seção não funciona. Instale o .NET Framework SDK. Depois de instalado, adicione o SDK à coleção e ao Sumário dos manuais online seguindo as instruções em [instalando o SDK do .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx).  
  
> [!NOTE]  
>  *Não* há suporte para a funcionalidade CLR, como funções de usuário CLR, para o banco de dados SQL do Azure.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Visão geral da integração do CLR&#41; &#40;Common Language Runtime](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
 Fornece uma visão geral breve do CLR e descreve como e por que essa tecnologia foi usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Descreve os benefícios de usar o CLR para criar objetos de banco de dados.  
  
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
 Descreve como os assemblies são usados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para implantar funções, procedimentos armazenados, gatilhos e agregações e tipos definidos pelo usuário, escritos em uma das linguagens de código gerenciado hospedadas pelo CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, e não escritos no [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Criando objetos de banco de dados com o Common Language Runtime &#40;integração de&#41; CLR](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)  
 Descreve os tipos de objetos que podem ser compilados usando o CLR e examina os requisitos para compilar objetos de banco de dados de CLR.  
  
 [Acesso aos dados dos objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
 Descreve como uma rotina de CLR pode acessar dados armazenados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
 Descreve o modelo de segurança da integração CLR.  
  
 [Depurando objetos de banco de dados CLR](../../relational-databases/clr-integration/debugging-clr-database-objects.md)  
 Descreve limitações e requisitos para depurar objetos de banco de dados de CLR.  
  
 [Implantando objetos de banco de dados CLR](../../relational-databases/clr-integration/deploying-clr-database-objects.md)  
 Descreve a implantação de assemblies para servidores de produção.  
  
 [Gerenciando assemblies de integração CLR](../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)  
 Descreve como criar e descartar assemblies de integração CLR.  
  
 [Monitorando e diagnosticando objetos de banco de dados gerenciado](../../relational-databases/clr-integration/monitoring-and-troubleshooting-managed-database-objects.md)  
 Fornece informações sobre as ferramentas que podem ser usadas para monitorar e solucionar problemas em objetos de bancos de dados gerenciados e assemblies que são executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Cenários de uso e exemplos para a integração do CLR &#40;Common Language Runtime&#41;](https://msdn.microsoft.com/library/33aac25f-abb4-4f29-af88-4a0dacd80ae7)  
 Descreve casos de uso e exemplos de códigos que usam objetos CLR.  
  
## <a name="see-also"></a>Consulte Também  
 [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Instalando o SDK do .NET Framework](https://technet.microsoft.com/library/bb686823\(v=SQL.105\).aspx)  
  
  
