---
title: Método setPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 297d37f6e0451e207d92dbc8a342b087c4d28895
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219365"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>Método setPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o tamanho do pacote de rede atual usado para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especificado em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *packetSize*  
  
 Um valor **int** que contém o tamanho do pacote de rede.  
  
## <a name="remarks"></a>Comentários  
 O intervalo de valores aceitáveis dessa propriedade é [-1 | 0 | 512..32767]. Se essa propriedade for definida como um valor fora do intervalo aceitável, ocorrerá uma exceção.  
  
 O aplicativo pode desejar definir a propriedade packetSize ao se conectar com a criptografia TLS, anteriormente conhecida como SSL. O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] negocia o tamanho do pacote com o servidor. Se a propriedade de criptografia for definida como "**true**" e o tamanho de pacote negociado for maior que o tamanho do registro TLS do provedor de segurança padrão da JVM (Máquina Virtual Java), o driver produzirá um erro e encerrará a conexão.  
  
 Além disso, o aplicativo poderá desejar definir a propriedade packetSize sem solicitar a criptografia TLS. Nesse caso, se o servidor exigir que o cliente dê suporte à criptografia TLS, o driver verificará o tamanho do registro TLS do provedor de segurança padrão da JVM. Se a propriedade packetSize for maior que o tamanho do registro TLS do provedor de segurança padrão da JVM, o driver produzirá um erro e encerrará a conexão.  
  
 Para obter mais informações sobre como usar o TLS, confira [Como usar a criptografia](../../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
