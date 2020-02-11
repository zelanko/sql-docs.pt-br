---
title: Instalando o SSMA para cliente DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/07/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1623430eed752db7fa387caf33124082eb318490
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70774182"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Instalando o SSMA para cliente DB2 (DB2ToSQL)

O cliente do SSMA consiste nos arquivos de programa que executam as seguintes tarefas:  
  
- Conecte-se a um banco de dados DB2.  
  
- Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Converta objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados DB2 em sintaxe.  
  
- Carregue os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Migre dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o.  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Prerequisites

O SSMA foi projetado para trabalhar com o DB2 no z/OS versão 9,0 e 10,0 ou DB2 no LUW versão 9,8 e 10,1 ou versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] posteriores e 2012 ou versões posteriores.  
  
Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:  
  
- Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou versões posteriores.  
  
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 ou posterior. A [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 está disponível na mídia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do produto. Você também pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
- Provedor Microsoft OLEDB para DB2 versão 5 ou uma versão posterior e conectividade com os bancos de dados DB2 que você deseja migrar.  
  
- Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure, onde você migrará os objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
- 4 GB de RAM recomendado.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Provedor Microsoft OLEDB para DB2  

Para baixar o provedor OLEDB para DB2 versão 6,0, vá para [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmafordb2).  
  
Depois de baixar a versão mais recente, extraia os arquivos de instalação para que você possa instalar o SSMA.  
  
Para instalar o cliente SSMA:
  
1. Clique duas vezes em SSMA para DB2 *n*. Install. exe, em que *n* é o número de Build.  
  
2. Sobre o **boas-vindas** página, selecione **próxima**.  
  
   Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.  
  
3. Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e, em seguida, selecione **Avançar**.  
  
4. Na página **escolher tipo de instalação** , selecione **típica**.  
  
5. Selecione **Instalar**.  
  
> [!IMPORTANT]  
> Desinstale todas as versões anteriores do SSMA para DB2 antes de instalar a nova versão.
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server for DB2.  
  
## <a name="see-also"></a>Confira também

[Instalando os componentes do SSMA em SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Migrar bancos de dados DB2 para SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
