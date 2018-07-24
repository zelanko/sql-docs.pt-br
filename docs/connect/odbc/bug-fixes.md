---
title: Lista de bugs corrigidos | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 3b5969a723b230139b9466f75569375f97a0d7b0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37946900"
---
# <a name="list-of-bugs-fixed"></a>Lista de bugs corrigidos

Esta página contém uma lista dos bugs corrigidos em cada versão, começando com [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversionmdmd"></a>Correções de bug no [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.2 do Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Corrigido uma mensagem de erro sobre a autenticação do Active Directory do Azure
- Detecção de codifica fixa quando variáveis de ambiente da localidade são definidas de forma diferente
- Correção de uma falha ao desconectar-se com a recuperação da conexão em andamento
- Fixa a detecção de atividade de conexão
- Fixa detecção incorreta de soquetes fechados
- Correção de uma espera infinita ao tentar liberar um identificador de instrução durante a recuperação com falha
- Corrigido o comportamento de desinstalação incorreto quando ambos os versão 13 e 17 estão instalados no Windows
- Comportamento de descriptografia fixo na plataforma do Windows mais antigo (Windows 7, 8 e Server 2012)
- Corrigido um problema de cache ao usar a autenticação ADAL em Windows
- Corrigido um problema que foi o bloqueio e substituir o rastreamento registra em log no Windows

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Correções de bug no [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.1 do Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Corrigido o atraso de 1 segundo ao chamar SQLFreeHandle com o MARS ativado e o atributo de conexão "Encrypt = yes"
- Corrigida uma falha de erro 22003 em SQLGetData quando o tamanho do buffer passado é menor, então os dados que estão sendo recuperados (Windows)
- Corrigido mensagens de erro ADAL truncado
- Corrigido um bug raro no Windows de 32 bits, durante a conversão flutuante número de ponto em um inteiro
- Corrigido um problema em que inserindo duplas no campo decimal com o Always Encrypted em retornar erro de truncamento de dados
- Corrigido um aviso no instalador do MacOS
- Corrigido o envio estado incorreto para o SQL Server durante a tentativa de recuperação de sessão quando a resiliência de Conexão e o Pooling de Conexão os dois estiverem habilitados, fazendo com que a sessão a ser descartado pelo servidor

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Correções de bug no [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Corrigido um bug em que ao usar a autenticação Kerberos, a inserção em massa poderá falhar com o erro "acesso negado"
- Solução alternativa removida para um bug de unixODBC presente na versão abaixo 2.3.1 (driver duplicado os tamanhos de determinados buffers passados para unixODBC)
- Corrigido resiliência de Conexão (reconexão) deslocado ao usar ColumnEncryption = habilitado
- Correção de bug de criação de DSN, onde quando usando "Autenticação interativa do Active Directory" a opção autenticação do Azure janela poderia ficar sem resposta (Windows)
- Corrigida uma falha de rara durante o desligamento do ODBC quando a execução assíncrona está habilitada (aconteceu ao limpar o identificador de conexão)
- Corrigido um problema em que o Driver do SQL causou alto consumo de CPU durante a execução de procedimentos armazenados de longo
- Correção da incapacidade de recuperar dados em uma coluna varbinary (max) criptografado sem conversão
- Corrigido um problema em que após um varchar nulo (max) coluna criptografada é obtida usando o SQLGetData () em um cursor estático, a coluna a seguir é também anulada, mesmo se ele tiver dados
- Corrigido um problema com buscando campo varbinary (max) com o Always Encrypted em
- Corrigido um problema de setlocale não funcionando com o Always Encrypted
- Corrigido um problema com SQLDescribeParam() retornando um erro quando chamado em um parâmetro de procedimento armazenado do tipo de XML com o Always Encrypted em
- Corrigido o escape sublinhados não está funcionando no SQLTables
- Corrigido um bug em que os dados hebraicos (varchar) são truncados quando retornado como caracteres largos no Linux
- Corrigido um problema com as consultas de Shift-JIS codificado char/varchar do aplicativo de UTF-8
- Corrigido o bug onde chamando SQLGetInfo com parâmetro SQL_DRIVER_NAME retornado Linux-estilo de nome de arquivo no MacOS
- Corrigido um problema em que o carregamento de dados de caractere do Windows-1252, usando entrada arquivos maior do que 32k bytes em colunas VARCHAR usando o utilitário BCP pode resultar em falhas
