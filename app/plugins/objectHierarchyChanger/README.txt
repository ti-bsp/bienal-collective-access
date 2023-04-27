objectHierarchyChangerPlugin

Descrição

Quando um objeto tem o seu tipo alterado ou é movido na hierarquia de classificação, seu IDNO é atualizado de acordo com as regras definidas em app/conf/multipart_id_numbering.conf.

Instalação

Copie a pasta objectHierarchyChanger para o diretório app/plugins do Collective Access.
Edite o arquivo objectHierarchyChanger.conf em objectHierarchyChangerPlugin/conf, alterando o valor do parâmetro "enabled" para 1. Acrescente ou remova tipos de objetos na configuração "restrictToTypes", se necessário.