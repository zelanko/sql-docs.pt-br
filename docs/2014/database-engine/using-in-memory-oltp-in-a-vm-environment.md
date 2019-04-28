---
title: Usando OLTP na memória em um ambiente de VM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 27ec7eb3-3a24-41db-aa65-2f206514c6f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f7f04b04792167fe9c4733f3e066c362f3cae4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843050"
---
# <a name="using-in-memory-oltp-in-a-vm-environment"></a>Usando OLTP na Memória em um Ambiente de VM
  A virtualização do servidor pode ajudá-lo a diminuir os custos operacionais e de capital com a TI, e atingir uma maior eficiência de TI com processos de provisionamento de aplicativo, manutenção, disponibilidade e backup/recuperação aprimorados. Com os avanços tecnológicos recentes, as cargas de trabalho de banco de dados complexas podem mais ser prontamente consolidadas usando a virtualização. Este tópico sobre as práticas recomendadas para usar o [!INCLUDE[hek_1](../includes/hek-1-md.md)] em um ambiente virtualizado.  
  
##  <a name="bkmk_memoryPreAllocation"></a> Pré-alocação de memória  
 Para a memória em um ambiente virtualizado, o melhor desempenho e o suporte aprimorado são considerações essenciais. Você deve ser capaz de alocar memória rapidamente para máquinas virtuais dependendo de seus requisitos (cargas de pico e fora de pico) e garantir que a memória não seja desperdiçada. O recurso de Memória Dinâmica do Hyper-V aumenta a agilidade sobre como a memória é alocada e gerenciada entre as máquinas virtuais executadas em um host.  
  
 Algumas práticas recomendadas para virtualizar e gerenciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisam ser alteradas ao virtualizar um banco de dados com tabelas com otimização de memória. Sem tabelas com otimização de memória, duas das práticas recomendadas são:  
  
-   Se você usar MIN_SERVER_MEMORY, será melhor atribuir somente a quantidade de memória necessária para que a memória suficiente permaneça para outros processos (impedindo a paginação).  
  
-   Não defina o valor de pré-alocação de memória muito alto. Caso contrário, outros processos podem não obter memória suficiente no momento em que a exigirem e isso pode levar à paginação de memória.  
  
 Se você seguir as práticas acima para um banco de dados com tabelas otimizadas pela memória, uma tentativa de restaurar e recuperar um banco de dados poderá resultar no banco de dados ficando em um estado de “Recuperação Pendente”, mesmo se você tiver memória suficiente para recuperá-lo. A razão para isso é que, ao iniciar, o [!INCLUDE[hek_2](../includes/hek-2-md.md)] coloca os dados na memória de maneira mais agressiva que a alocação dinâmica de memória aloca a memória para o banco de dados.  
  
 **Resolução**  
  
 Para solucionar isso, pré-aloque memória suficiente para o banco de dados a ser recuperado ou reinicie o banco de dados, não um valor mínimo que depende da memória dinâmica para fornecer a memória adicional quando for necessário.  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
