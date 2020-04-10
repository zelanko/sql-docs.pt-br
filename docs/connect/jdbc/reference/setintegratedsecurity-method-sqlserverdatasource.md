---
title: Método setIntegratedSecurity (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3c01360160093465919625757e29602494860f2f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922245"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>Método setIntegratedSecurity (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **booliano** que indica se a propriedade integratedSecurity está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *enable*  
  
 **true** se integratedSecurity estiver habilitado. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Defina como "**true**" para indicar que as credenciais do Windows serão usadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para autenticar o usuário do aplicativo. Se "**true**", o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] pesquisará no cache de credenciais do computador local as credenciais que já foram fornecidas quando foi feito logon no computador ou na rede. Se "**false**", o nome de usuário e a senha deverão ser fornecidos.  
  
> [!NOTE]  
>  Essa propriedade só é compatível nos sistemas operacionais [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows.  
  
 Para obter mais informações sobre o uso da autenticação integrada, confira [Como criar a URL de conexão](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
