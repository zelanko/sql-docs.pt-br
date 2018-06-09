---
title: Práticas recomendadas para o Assistente de migração de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 8a1b184a6a280b328df35ea04a1ab6caf996c7c8
ms.sourcegitcommit: 6fe7b5e8818bd0d94fce693c560d63cc6883d76f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34758106"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Práticas recomendadas para executar o Assistente de migração de dados
Este artigo fornece as seguintes informações de práticas recomendadas para a migração, avaliação e instalação.

## <a name="installation"></a>Instalação
Não instale e execute o Assistente de migração de dados diretamente no computador de host do SQL Server.

## <a name="assessment"></a>Avaliação
- Execute avaliações em bancos de dados de produção durante horários de pico.
- Executar o **problemas de compatibilidade** e **novas recomendações de recurso** avaliações separadamente para reduzir a duração de avaliação.

## <a name="migration"></a>Migração
- Migre um servidor durante horários de pico.
- Ao migrar um banco de dados, forneça um local único compartilhamento acessível pelo servidor de origem e o servidor de destino e evite uma operação de cópia, se possível. Uma operação de cópia pode introduzir um atraso com base no tamanho do arquivo de backup. A operação de cópia também aumenta as chances de que a migração falhará devido a uma etapa extra. Quando é fornecido um único local, o Assistente de migração de dados ignora a operação de cópia.
 
    Além disso, certifique-se que fornecer as permissões corretas para a pasta compartilhada para evitar falhas de migração. As permissões corretas são especificadas na ferramenta. Se uma instância do SQL Server for executado sob as credenciais do serviço de rede, conceda as permissões corretas na pasta compartilhada para a conta do computador para a instância do SQL Server.

- Habilitar criptografar a conexão ao conectar-se aos servidores de origem e destino. Uso de SSL criptografia aumenta a segurança dos dados transmitidos pelas redes entre o Assistente de migração de dados e a instância do SQL Server, que é útil principalmente ao fazer a migração de logons do SQL Server. Se a criptografia SSL não é usada e a rede está comprometida por um invasor, os logons do SQL Server que está sendo migrados podem obter interceptadas e/ou modificado em dinamicamente pelo invasor.

    No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. Habilitando a criptografia reduz o desempenho porque a sobrecarga extra que é necessária para criptografar e descriptografar os pacotes. Para obter mais informações, consulte [criptografando conexões com o SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
