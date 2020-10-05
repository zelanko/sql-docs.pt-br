---
title: Melhores práticas para o Assistente de Migração de Dados
description: Conheça as práticas recomendadas para migrar SQL Server bancos de dados com Assistente de Migração de Dados, incluindo informações sobre instalação, avaliação e migração.
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 440d6d12ed639d158ad0309209b60daa56e08322
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727777"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Melhores práticas para a execução do Assistente de Migração de Dados
Este artigo fornece algumas informações de práticas recomendadas para instalação, avaliação e migração.

## <a name="installation"></a>Instalação
Não instale e execute o Assistente de Migração de Dados diretamente na máquina host SQL Server.

## <a name="assessment"></a>Avaliação
- Execute avaliações em bancos de dados de produção fora do horário de pico.
- Execute os **problemas de compatibilidade** e as novas avaliações de **recomendações de recursos** separadamente para reduzir a duração da avaliação.

## <a name="migration"></a>Migração
- Migre um servidor fora do horário de pico.

- Ao migrar um banco de dados, forneça um único local de compartilhamento acessível pelo servidor de origem e pelo servidor de destino e evite uma operação de cópia, se possível. Uma operação de cópia pode introduzir um atraso com base no tamanho do arquivo de backup. A operação de cópia também aumenta as chances de uma migração falhar devido a uma etapa extra. Quando um único local é fornecido, Assistente de Migração de Dados ignora a operação de cópia.
 
    Além disso, certifique-se de fornecer as permissões corretas para a pasta compartilhada para evitar falhas de migração. As permissões corretas são especificadas na ferramenta. Se uma instância de SQL Server for executada em credenciais de serviço de rede, conceda as permissões corretas na pasta compartilhada à conta do computador para a instância de SQL Server.

- Habilite a conexão criptografada ao conectar-se aos servidores de origem e de destino. O uso da criptografia TLS aumenta a segurança dos dados transmitidos pelas redes entre Assistente de Migração de Dados e a instância de SQL Server, o que é benéfico especialmente ao migrar logons do SQL. Se a criptografia TLS não for usada e a rede estiver comprometida por um invasor, os logons do SQL que estão sendo migrados poderão ser interceptados e/ou modificados imediatamente pelo invasor.

    No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. A habilitação da criptografia reduz o desempenho porque a sobrecarga extra é necessária para criptografar e descriptografar pacotes. Para obter mais informações, consulte [Criptografando conexões com SQL Server](/previous-versions/sql/sql-server-2008-r2/ms189067(v=sql.105)).
    
- Verifique se há restrições não confiáveis no banco de dados de origem e no de destino antes de migrá-los. Após a migração, analise o banco de dados de destino novamente para ver se alguma restrição se tornou não confiável como parte da movimentação de dados. Corrija as restrições não confiáveis conforme necessário. Deixar as restrições não confiáveis pode resultar em planos de execução insatisfatórios e pode afetar o desempenho.