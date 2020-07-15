---
title: Opção de configuração de servidor clr enabled | Microsoft Docs
description: Saiba como usar a opção clr enabled para especificar se o SQL Server pode executar assemblies de usuário. Veja quando não há suporte para a execução de Common Language Runtime.
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 56ddc21a660ba8316a9c311546e4ced48067f270
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759161"
---
# <a name="clr-enabled-server-configuration-option"></a>Opção clr enabled de configuração de servidor
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção clr habilitado para especificar se assemblies de usuário podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção clr enabled fornece os seguintes valores: 
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Execução de assembly não permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|1|Execução de assembly permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
Somente WOW64. Reinicie os servidores WOW64 para fazer com que as alterações de configurações tenham efeito. A reinicialização não é necessária para outros tipos de servidores.  

Ao executar RECONFIGURE e o valor de execução da opção clr enabled é alterado de 1 para 0, todos os domínios de aplicativo que contêm assemblies de usuário são descarregados imediatamente.  
  
>  **Não há suporte à execução de CLR (Common Language Runtime) com lightweight pooling** Desabilite uma das duas opções: "clr enabled" ou "lightweight pooling". Os recursos que dependem do CLR e que não funcionam corretamente no modo fibra incluem o tipo de dados **hierarchyid**, a função `FORMAT`, a replicação e o gerenciamento baseado em políticas.  
> 
> [!WARNING]
>  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. Um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios sysadmin. A partir do [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A `clr strict security` está habilitada por padrão e trata assemblies `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. A Microsoft recomenda que todos os assemblies sejam assinados por um certificado ou uma chave assimétrica com um logon correspondente que recebeu a permissão `UNSAFE ASSEMBLY` no banco de dados mestre. Os administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também podem adicionar assemblies a uma lista de assemblies, na qual o Mecanismo de Banco de Dados deve confiar. Para obter mais informações, consulte [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir primeiro mostra a configuração atual da opção clr enabled e, em seguida, habilita a opção configurando o valor da opção como 1. Para desabilitar a opção, defina o valor para 0.  
  
```sql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## <a name="see-also"></a>Consulte Também  
 [Opção lightweight pooling de configuração de Servidor](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção lightweight pooling de configuração de Servidor](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  
