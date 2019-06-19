---
title: Propriedades do servidor (página Memória) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: f5e1f10913f50363f41c086abb4f2ea1c4433c1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66783252"
---
# <a name="server-properties---memory-page"></a>Propriedades do servidor – página Memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use essa página para exibir ou modificar as opções de memória do servidor. Quando a **Memória mínima do servidor** está definida como 0 e a **Memória máxima do servidor** está definida como 2147483647 MB, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode tirar vantagem da quantidade ideal de memória a qualquer momento, sujeito à quantidade de memória que o sistema operacional e os outros aplicativos estão usando no momento. À medida que muda a carga no computador e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a memória alocada também muda. Você pode limitar mais essa alocação de memória dinâmica aos valores mínimo e máximo especificados abaixo.  
  
## <a name="options"></a>Opções  
 **Memória mínima do servidor (em MB)**  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve iniciar com pelo menos a quantidade mínima de memória alocada e não liberar memória abaixo desse valor. Defina esse valor com base no tamanho e na atividade de sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre defina a opção como um valor razoável para garantir que o sistema operacional não exija muita memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e iniba o desempenho do Windows.  
  
 **Memória máxima do servidor (em MB)**  
 Especifica a quantidade máxima de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode alocar quando inicia e enquanto está sendo executado. Essa opção de configuração pode ser definida como um valor específico, caso você tenha ciência de que há vários aplicativos em execução ao mesmo tempo como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e queira garantir que eles tenham memória suficiente para execução. Se esses outros aplicativos, tais como servidores Web ou de email, solicitarem memória apenas conforme necessário, não defina a opção, pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá liberar memória para eles conforme necessário. Muitas vezes, contudo, os aplicativos usam qualquer memória disponível ao serem iniciados e não solicitam mais quando necessário. Se um aplicativo que se comporta dessa maneira estiver em execução no mesmo computador e ao mesmo tempo em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], defina a opção com um valor que garanta que a memória solicitada pelo aplicativo não seja alocada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A quantidade mínima de memória que você pode especificar para a **memória máxima do servidor** é 128 MB. (64 MB (megabytes) para sistemas de 32 bits mais antigos.)  
  
 **Memória de criação de índice (em KB, 0 = memória dinâmica)**  
 Especifica a quantidade de memória (em KB) para usar durante as classificações de criação de índice. O valor padrão 0 permite a alocação dinâmica e deve funcionar na maioria dos casos sem ajustes adicionais, embora o usuário possa digitar um valor diferente de 704 a 2147483647.  
  
> [!NOTE]  
>  Não são permitidos valores de 1 a 703. Se for digitado um valor nesse intervalo, o campo substituirá o valor digitado por 704.  
  
 **Memória mínima por consulta (em KB)**  
 Especifica a quantidade de memória (em KB) para alocar a execução de uma consulta. O usuário pode definir o valor de 512 a 2147483647 KB. O valor padrão é 1024 KB.  
  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se não houver nenhum, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser reiniciada.  
  
 **Executando Valores**  
 Mostra os valores que estão sendo executados para as opções nesse painel. Esses valores são somente leitura.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
