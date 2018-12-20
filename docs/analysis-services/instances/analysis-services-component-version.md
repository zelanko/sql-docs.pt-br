---
title: Verifique se a versão de compilação de atualização cumulativa do SQL Server Analysis Services | Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: 87efa581f7d4d84e9e5c05690ee1cb43bd4532dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38999346"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>Verifique se a versão de compilação do Analysis Services atualização cumulativa

Começando com o SQL Server 2017, o número de versão de compilação do Analysis Services e o número de versão de compilação do mecanismo de banco de dados do SQL Server não coincidem. Embora o Analysis Services e o mecanismo de banco de dados usam o mesmo instalador, os sistemas de build cada uso são separadas.

 Em alguns casos, ele pode ser necessário verificar se um pacote de compilação da atualização cumulativa (AC) foi aplicado e os componentes do Analysis Services foram atualizados. Você pode verificar, comparando os números de versão de compilação de arquivos de componentes do Analysis Services instalados no computador com os números de versão de compilação para uma determinada atualização cumulativa.

## <a name="verify-component-file-version"></a>Verifique se a versão do arquivo de componente

Para verificar a versão do arquivo de componente, 

1. Vá para [versões de compilação do SQL Server 2017](https://support.microsoft.com/help/4047329). 
2. Na **compilações do SQL Server 2017 de atualização cumulativa (AC)**, clique no **número da Base de dados de Conhecimento** para a compilação que você deseja verificar.
3. No **atualização cumulativa (#) para o SQL Server 2017** artigo, o **informações do pacote de atualização cumulativa** seção, expanda **informações de arquivo de pacote de atualização cumulativa**.
4. No **SQL Server 2017 Analysis Services** da tabela, verifique a versão do arquivo para o **msmdsrv.exe** arquivo de componente. Se o valor de atualização cumulativa tiver sido aplicada, o número de versão do arquivo deve corresponder o arquivo msmdsrv.exe instalado em seu computador.

## <a name="see-also"></a>Confira também  

[Instalar atualizações de serviço do SQL Server](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Centro de atualização do Microsoft SQL Server](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
