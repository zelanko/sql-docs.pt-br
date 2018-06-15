---
title: Configurar o Windows para receber cópias da tabela remota - Parallel Data Warehouse | Microsoft Docs
description: Descreve como adquirir e configurar um sistema do Windows não seja de aplicação conectado usando a rede InfiniBand para uso com o recurso de cópia da tabela remota no Parallel Data Warehouse. O sistema do Windows irá hospedar o banco de dados do SQL Server que recebe a cópia da tabela remota de um banco de dados do SQL Server PDW. É adquirida separadamente do dispositivo e conectado à rede InfiniBand appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ed7122f497b0bdebd893eec75606bbb6382e9a73
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538766"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configurar um sistema externo do Windows para receber cópias da tabela remota usando InfiniBand - Parallel Data Warehouse
Descreve como adquirir e configurar um sistema do Windows não seja de aplicação conectado usando a rede InfiniBand para uso com o recurso de cópia da tabela remota no SQL Server PDW. O sistema do Windows irá hospedar o banco de dados do SQL Server que recebe a cópia da tabela remota de um banco de dados do SQL Server PDW. É adquirida separadamente do dispositivo e conectado à rede InfiniBand appliance.  
  
> [!NOTE]  
> Conectando por meio da rede InfiniBand não é necessário para usar a cópia da tabela remota. Conectando por meio da rede de Ethernet pode ser feito se a largura de banda de Ethernet atende às suas necessidades.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia da tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Antes de começar  
Antes de configurar o sistema externo do Windows, você deve:  
  
1.  Comprar ou fornecer um sistema Windows que receberá as cópias remotas.  
  
2.  O sistema do Windows no rack controle de rack (se houver espaço suficiente) ou feche suficiente para o dispositivo para que você pode conectá-lo à rede InfiniBand appliance.  
  
3.  Comprar InfiniBand cabos e um adaptador de rede InfiniBand de seu fornecedor de hardware do dispositivo. Recomendamos que você comprar um adaptador de rede com duas portas para tolerância a falhas ao receber os dados exportados. Um adaptador de rede de duas portas é recomendado, mas não é um requisito.  
  
## <a name="HowToWindows"></a>Configure um sistema Windows externo para receber cópias da tabela remota  
Para configurar o sistema externo do Windows, use as seguintes etapas:  
  
1.  Instale o adaptador de rede InfiniBand no seu sistema Windows.  
  
2.  Conecte o adaptador de rede InfiniBand ao comutador InfiniBand principal no rack controle usando cabos do InfiniBand.  
  
3.  Instale e configure o driver apropriado do Windows para o adaptador de rede InfiniBand.  
  
    InfiniBand drivers do Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio do setor de fornecedores de InfiniBand.  O driver correto pode foram distribuído com o adaptador do InfiniBand. Caso contrário, o driver pode ser baixado do www.openfabrics.org.  
  
4.  Configure o endereço IP para cada porta do adaptador. Sistemas SMP são necessários para usar endereços IP estáticos de um intervalo de endereços reservados para essa finalidade. Configure a primeira porta de acordo com os seguintes parâmetros:  
  
    -   Endereço de rede IP: 172.16.132.x  
  
    -   Máscara de sub-rede IP: 255.255.128.0  
  
    -   Intervalo IP de host: 1-254  
  
    Para adaptadores de rede InfiniBand com duas portas, configure a segunda porta de acordo com os seguintes parâmetros:  
  
    -   Endereço de rede IP: 172.16.132.x  
  
    -   Máscara de sub-rede IP: 255.255.128.0  
  
    -   Intervalo IP de host: 1-254  
  
5.  Se um adaptador de duas portas é usado ou vários sistemas externos estão conectados a um dispositivo, atribua um número de host diferente em cada sub-rede IP para cada sistema.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
