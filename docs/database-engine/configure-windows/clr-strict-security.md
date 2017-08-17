---
title: "Segurança estrita do CLR | Microsoft Docs"
description: "Como configurar a segurança estrita do CLR no SQL Server"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- clr strict security
- clr_strict_security_TSQL
- clr strict security
- strict_security_TSQL
helpviewer_keywords:
- assemblies [CLR integration], strick security
- clr strict security option
ms.assetid: 
caps.latest.revision: 0
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 54f976fac931d9cdc731f4b3e91c433d66310194
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="clr-strict-security"></a>Segurança estrita do CLR   
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]   

Controla a interpretação das permissões `SAFE`, `EXTERNAL ACCESS` e `UNSAFE` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   

|Valor |Descrição | 
|----- |----- | 
|0 |Desabilitado – fornecido para fins de compatibilidade com versões anteriores. O valor `Disabled` não é recomendado. | 
|1 |Habilitado – faz com que o [!INCLUDE[ssde-md](../../includes/ssde-md.md)] ignore as informações de `PERMISSION_SET` sobre os assemblies e sempre interprete-as como `UNSAFE`.  `Enabled` é o valor padrão do [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]. | 

>  [!WARNING]
>  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. Um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios sysadmin. A partir do [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A `clr strict security` está habilitada por padrão e trata assemblies `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. A Microsoft recomenda que todos os assemblies sejam assinados por um certificado ou uma chave assimétrica com um logon correspondente que recebeu a permissão `UNSAFE ASSEMBLY` no banco de dados mestre. Os administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também podem adicionar assemblies a uma lista de assemblies, na qual o Mecanismo de Banco de Dados deve confiar. Para obter mais informações, consulte [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md).

## <a name="remarks"></a>Comentários   

Quando habilitada, a opção `PERMISSION_SET` nas instruções `CREATE ASSEMBLY` e `ALTER ASSEMBLY` é ignorada em tempo de execução, mas as opções `PERMISSION_SET` são preservadas nos metadados. Ignorar a opção minimiza a interrupção de instruções de código existentes.

`CLR strict security` é um `advanced option`.  

>  [!IMPORTANT]  
>  Depois de habilitar segurança estrita, os assemblies que não estão assinados não serão carregados. Você deve alterar ou remover e recriar cada assembly, de modo que ele seja assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor.

## <a name="permissions"></a>Permissões 

### <a name="to-change-this-option"></a>Para alterar essa opção  
Exige a permissão `CONTROL SERVER` ou a associação na função de servidor fixa `sysadmin`.

### <a name="to-create-an-clr-assembly"></a>Para criar um assembly CLR   
As seguintes permissões necessárias para criar um assembly CLR quando o `CLR strict security` está habilitado:

- O usuário deve ter a permissão `CREATE ASSEMBLY`  
- Além disso, uma das seguintes condições também deve ser verdadeira:  
  - O assembly é assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. A assinatura do assembly é recomendada.  
  - O banco de dados tem a propriedade `TRUSTWORTHY` definida como `ON` e o banco de dados pertence a um logon que tem a permissão `UNSAFE ASSEMBLY` no servidor. Essa opção não é recomendada.  

  
## <a name="see-also"></a>Consulte também  
  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opção de configuração do servidor clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)

