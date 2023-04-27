Descrição das alterações em relação às configurações originais
--------------------------------------------------------------

A) app.conf

session_lifetime = 60000

nav_config = <ca_conf_dir>/local/navigation.conf

field_label_defs = <ca_conf_dir>/field_labels.conf

# Fonts to use for PDF generation
fonts_directory = <ca_app_dir>/fonts
ca_objects_print_forms = <ca_conf_dir>/ca_objects_label_layouts.conf
ca_object_lots_print_forms = <ca_conf_dir>/ca_object_lots_label_layouts.conf
ca_collections_print_forms = <ca_conf_dir>/ca_collections_label_layouts.conf
ca_loans_print_forms = <ca_conf_dir>/ca_loans_label_layouts.conf
ca_movements_print_forms = <ca_conf_dir>/ca_movements_label_layouts.conf
ca_storage_locations_print_forms = <ca_conf_dir>/ca_storage_locations_label_layouts.conf

allow_duplicate_id_number_for_ca_objects = 0

allow_duplicate_labels_for_ca_entities = 1
allow_duplicate_labels_for_ca_collections= 1
allow_duplicate_labels_for_ca_occurrences= 1


use_legacy_print_labels_generator = 0

enable_library_services = 1
enable_object_checkout = 1

always_use_session_based_storage_for_find_result_contexts = 1


A) authentication.conf

auth_allow_password_reset de 0 para 1

-------------------------------------

B) browse.conf

defaultHitsPerBlock = 36

Facets criados:

objetos:

document_genre
document_type
document_support
entities_author
acqinfo_entity_source
occurrences_production
nat_representation
tipo_cromia
tipo_polaridade
bienal_awards
authorplace
has_award
city_country_countryvalue
city_country_cityvalue

entidades:

entity_category
birthplace
participation
participation_facet_section
award

ocorrências:

event_type_value
event_type_bienal
realizacao
local
repnacplace
pesquisador
entidade_pesquisada


Facets desabilitados, excluídos ou adaptados

objetos

title
violation
checkouts
deaccession
entity
place
collection
occurrences
storage_location
term
status
access

entidades

place
occurrence
collection
term
status
access
has_media

ocorrências

entity
place
occurrence
term
status
acesss
has_media

object representations

title
entity
place
collection
occurrence
storage_location
term

-------------------------------------

C) library_services.conf

Novo checkout_type = copy

Em cada item de panels, group_by = {ca_objects.library_formats, ca_objects.parent.library_formats}

restrict_to_circulation_statuses = [available]

-------------------------------------

D) multipart_id_numbering.conf

Formatos de IDNO configurados:

- para ca_objects:
	fonds
	collections
	groups
	subgroups
	series
	file
	documents
	document_parts
	artworks
	
- para ca_entities:
	formato __default__ alterado
	
- para ca_occurrence:
	formato __default__ alterado
	pesquisa
	
-------------------------------------

E) media_display.conf

Em media_overlay => images

exclusão de image/gif, image/bmp e image/x-bmp de mimetypes.

use_book_viewer_when_number_of_representations_exceeds = 2
use_book_viewer = 1
show_hierarchy_in_book_viewer = 1
show_subhierarchy_in_book_viewer = 1
restrict_book_viewer_to_types = []

exclusão dos parâmetros

no_overlay = 1
viewer = TileViewer,
use_mirador_for_image_list_length_at_least = 3

Em media_overlay

adição de gif

Em media_overlay => video e video_h264_original

viewer_height = 95%
exclusão de viewer = VideoJS

Em media_overlay => quicktimevr =

exclusão de viewer = QTVR

Em media_overlay => audio

exclusão de audio/x-flac de mimetypes

exclusão de viewer = MediaElement

--------------------------------------

F) navigation.conf

Em navigation -> "New" -> navigation:

"occurrences_editor"
	"hide" = 1
	
	"requires" = {
					action:can_create_ca_occurrences = AND,
 					configuration:!ca_occurrences_disable = AND,
 					configuration:!ca_occurrences_dont_show_in_new_menu = AND
 				}
				
Em navigation -> "find" -> navigation:

"object_lots"
	"requires" = {
					action:can_search_ca_object_lots = OR,
					action:can_browse_ca_object_lots = OR,
 					configuration:!ca_object_lots_disable = AND, configuration:!ca_object_lots_breakout_find_by_type_in_menu = AND, availableTypes:ca_object_lots:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}
				
"objects"
	"requires" = {
					action:can_search_ca_objects = OR,
					action:can_browse_ca_objects = OR,
 					configuration:!ca_objects_disable = AND, configuration:!ca_objects_breakout_find_by_type_in_menu = AND, availableTypes:ca_objects:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}

"object_representations"
	"requires" = {
					action:can_search_ca_object_representations = OR,
					action:can_browse_ca_object_representations = OR,
 					configuration:!ca_object_representations_disable = AND, configuration:!ca_object_representations_dont_show_in_find_menu = AND, configuration:!ca_object_representations_breakout_find_by_type_in_menu = AND, availableTypes:ca_object_representations:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}

"entities"
	"requires" = {
					action:can_search_ca_entities = OR,
					action:can_browse_ca_entities = OR,
 					configuration:!ca_entities_disable = AND, configuration:!ca_entities_breakout_find_by_type_in_menu = AND, availableTypes:ca_entities:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}

"places"
	"requires" = {
					action:can_search_ca_places = OR,
					action:can_browse_ca_places = OR,
 					configuration:!ca_places_disable = AND, configuration:!ca_places_breakout_find_by_type_in_menu = AND, availableTypes:ca_places:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}
				
"collections"
	"requires" = {
					action:can_search_ca_collections = OR,
					action:can_browse_ca_collections = OR,
 					configuration:!ca_collections_disable = AND, configuration:!ca_collections_breakout_find_by_type_in_menu = AND, availableTypes:ca_collections:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}

"occurrences"
	"requires" = {
					action:can_search_ca_occurrences = OR,
					action:can_browse_ca_occurrences = OR,
 					configuration:!ca_occurrences_disable = AND, configuration:!ca_occurrences_breakout_find_by_type_in_menu = AND, availableTypes:ca_occurrences:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}

"storage_locations"
	"requires" = {
					action:can_search_ca_storage_locations = OR,
					action:can_browse_ca_storage_locations = OR,
 					configuration:!ca_storage_locations_disable = AND, configuration:!ca_storage_locations_breakout_find_by_type_in_menu = AND, availableTypes:ca_storage_locations:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}
				
"loans" 
	"requires" = {
					action:can_search_ca_loans = OR,
					action:can_browse_ca_loans = OR,
 					configuration:!ca_loans_disable = AND, configuration:!ca_loans_breakout_find_by_type_in_menu = AND, availableTypes:ca_loans:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}
				
"movements"
	"requires" = {
					action:can_search_ca_movements = OR,
					action:can_browse_ca_movements = OR,
 					configuration:!ca_movements_disable = AND, configuration:!ca_movements_breakout_find_by_type_in_menu = AND, availableTypes:ca_movements:__CA_BUNDLE_ACCESS_READONLY__ = AND
				}
				
				
Em navigation -> "manage" -> "navigation" -> "navigation" -> "duplication" -> navigation:

"collections"
	"requires" = {
					configuration:!ca_occurrences_disable = AND,
					action:can_duplicate_ca_occurrences = AND
				}

Em navigation -> "manage" -> "navigation" -> "search_tools" -> "navigation"

"search_forms"
"requires" = {
				action:can_set_access_control = AND								  
			}

"saved_searches"
"requires" = {
				action:can_set_access_control = AND
			}
			
"user_sorts"
	[exclusão do "requires"]
	

Em navigation -> "manage" -> "navigation" -> "pawtucket" -> "navigation"

"Global values" 
"requires" = {
				action:can_edit_theme_global_values = OR
			}

Em navigation -> "Import"

"requires" = {
				action:can_batch_import_media = OR
			}

Em navigation -> "Import" -> "navigation"

"batch_media_import"
"requires" = {

			}
			
"batch_metadata_import"
"requires" = {

			}

Em navigation -> "Import" -> "navigation" -> "batch_media_import" -> "navigation"

"mediaImport"
"requires" = {

			}
			
Em navigation -> "Import" -> "navigation" -> "batch_metadata_import" -> "navigation"

"metadata_importer_list"
"requires" = {

			}
						
"metadata_import_run" 
"requires" = {

			}
--------------------------------------

G) search.conf

cache_timeout = 300
search_sql_search_do_stemming = 0
indexing_tokenizer_regex = ^\pL\pN\pNd/_#\@\&\-\.
search_tokenizer_regex = ^\pL\pN\pNd/_#\@\&\-\.

--------------------------------------

G) search_indexing.conf

Access points criados:

- para ca_objects
	parent_id
	artisticProcess
	cityCountry
	evento_relacionado
	
- para ca_occurrences
	evento_bienal
	pesquisador
	entidade_pesquisada
	evento_pesquisado

Definição de campos pesquisáveis

- para ca_objects
	idno
	type_id
	parent_id
	source_id
	hier_object_id
	access
	status
	deleted
	is_deaccessioned
	deaccession_notes
	deaccession_date
	preferred_labels
	_ca_attribute_unitdate
	_ca_attribute_production_date
	_ca_attribute_document_genre
	_ca_attribute_document_type
	_ca_attribute_analog_digital
	_ca_attribute_form
	_ca_attribute_inscription
	_ca_attribute_other_identification_form
	_ca_attribute_others_idno
	_ca_attribute_document_support
	_ca_attribute_document_technique
	_ca_attribute_artwork_support
	_ca_attribute_artwork_technique
	_ca_attribute_artwork_type
	_ca_attribute_art_form
	_ca_attribute_artwork_material_support
	_ca_attribute_artwork_technique_process
	_ca_attribute_artwork_description
	_ca_attribute_location_identifier
	_ca_attribute_storage_note
	_ca_attribute_acqinfo
	_ca_attribute_acqinfo.acqinfo_entity_source
	_ca_attribute_acqinfo.acqinfo_acq_type
	_ca_attribute_acqinfo.acqinfo_entry_date
	_ca_attribute_acqinfo.acqinfo_acquisition_date
	_ca_attribute_acqinfo.acqinfo_acquisition_details
	_ca_attribute_city_country
	_ca_attribute_city_country.city_country_countryvalue
	_ca_attribute_city_country.city_country_cityvalue
	_ca_attribute_nat_representation
	_ca_attribute_content_description
	_ca_attribute_physaccessrestrict 
	_ca_attribute_langmaterial 
	_ca_attribute_langmaterial.lang_material_lang 
	_ca_attribute_conservation_status
	_ca_attribute_conservation_status.treatment_status_value 
	_ca_attribute_conservation_status.conservation_value 
	_ca_attribute_conservation_damagetype
	_ca_attribute_conservation_damagetype.conservation_damagetype_val
	_ca_attribute_conservation_intervention
	_ca_attribute_conservation_intervention.intervention_value
	_ca_attribute_conservation_intervention.intervention_performed
	_ca_attribute_conservation_packaging
	_ca_attribute_conservation_packaging.conservation_packaging_primary
	_ca_attribute_conservation_packaging.conservation_packaging_second
	_ca_attribute_conservation_packaging.conservation_packaging_third
	_ca_attribute_conservation_note
	_ca_attribute_conservation_note.conservation_note_value
	_ca_attribute_conservation_note.conservation_note_date
	_ca_attribute_conservation_note.conservation_dates_types
	_ca_attribute_conservation_note.conserv_note_responsable
	_ca_attribute_note
	_ca_attribute_demands_normalization
	_ca_attribute_review_pendencies
	_ca_attribute_tipo_cromia
	_ca_attribute_tipo_polaridade
	_ca_attribute_tipo_midia
	_ca_attribute_padrao_gravacao
	_ca_attribute_biblio_location_type
	_ca_attribute_biblio_location_subject
	_ca_attribute_biblio_location_PHA
	_ca_attribute_controle_importacao
	related
	
	ca_object_labels
	ca_entities
	ca_entity_labels
	ca_places
	ca_place_labels
	ca_occurrences
	ca_objects_x_occurrences
	ca_objects_x_entities
	ca_occurrence_labels
	ca_collections
	ca_collection_labels
	ca_loan_labels
	ca_loans
	ca_list_items
	ca_list_item_labels
	ca_representation_annotation_labels
	ca_item_tags
	ca_sets
	ca_storage_locations
	ca_storage_location_labels
	ca_object_representations
	
- para ca_entities
	ca_entity_labels
	ca_place_labels
	ca_occurrence_labels
	ca_entities_x_occurrences
	ca_objects
	ca_object_labels
	ca_collection_labels
	ca_list_item_labels
	ca_sets
	
- para ca_occurrences
	ca_occurrence_labels
	ca_entities
	ca_entity_labels
	ca_objects
	ca_object_labels
	ca_entities_x_occurrences
	ca_places
	ca_place_labels
	ca_collections
	ca_collection_labels
	ca_list_item_labels
	ca_sets
	
- para ca_object_representations
	ca_object_representation_labels
	ca_object_labels
	ca_objects
	ca_entities
	ca_entity_labels
	ca_place_labels
	ca_occurrence_labels
	ca_list_item_labels
	ca_collection_labels
	ca_storage_location_labels
	

