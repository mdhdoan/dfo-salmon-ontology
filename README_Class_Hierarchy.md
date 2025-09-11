# Salmon Inspections Ontology — Class Hierarchy

_Generated: 2025-09-11T22:20:03_

- Files merged: draft_salmon_information_FIXED_AUTOPATCH_v2.ttl, draft_environment_information_FIXED_AUTOPATCH_v2.ttl, draft_inspection_information_FIXED_AUTOPATCH_v2.ttl

- Total triples: 869

## Classes

- **:Environmental** — "Environmental Factors"
  - **:LenticWaterBody** — "Lentic Water Body"
    _def:_ Standing or still freshwater ecosystems.
    - **:Lake** — "Lake"
      _def:_ A relatively large, inland body of standing water.
    - **:Pond** — "Pond"
      _def:_ A small, still body of water, generally smaller than a lake.
  - **:LoticWaterBody** — "Lotic Water Body"
    _def:_ Flowing freshwater ecosystems, such as rivers, streams, and creeks.
    - **:Creek** — "Creek"
      _def:_ A small, narrow freshwater channel; typically smaller than a stream.
    - **:River** — "River"
      _def:_ A large, natural flow of water moving within a channel toward an ocean, lake, or another river.
    - **:Slough** — "Slough"
      _def:_ A slow-moving side channel or backwater, often associated with floodplains or wetlands.
    - **:Stream** — "Stream"
      _def:_ A body of flowing water larger than a creek but smaller than a river.
  - **:StreamCondition** — "Stream Condition"
    _def:_ Dynamic states or disturbances affecting the stream or river at the time of inspection.
    - **:BankErosion** — "Bank Erosion"
      _def:_ The wearing away of stream banks by flowing water, weather, or human activity.
    - **:Debris** — "Debris"
      _def:_ Material such as woody debris, sediment, or human-made waste present in the stream channel.
    - **:Drought** — "Drought"
      _def:_ A prolonged period of deficient water flow in streams due to low precipitation.
    - **:Flood** — "Flood"
      _def:_ Overflow of water that submerges normally dry streambanks or floodplains.
    - **:SlopeInstability** — "Slope Instability"
      _def:_ Loss of stability in stream banks or adjacent slopes leading to erosion or landslides.
    - **:StreamObstruction** — "Stream Obstruction"
      _def:_ Physical barriers or blockages impeding the natural flow of a stream.
      - **:ObstructionOrigin** — "Obstruction Origin"
        _def:_ Classification of a stream obstruction based on whether it is natural or artificial.
        - **:ArtificialObstruction** — "Artificial Obstruction"
          _def:_ An obstruction resulting from human-made structures or debris, such as culverts, dams, or weirs.
        - **:NaturalObstruction** — "Natural Obstruction"
          _def:_ An obstruction created by natural processes such as log jams, beaver dams, or landslides.
      - **:ObstructionPassability** — "Obstruction Passability"
        _def:_ Classification of a stream obstruction based on whether fish can pass it.
        - **:Impassable** — "Impassable"
          _def:_ An obstruction that fully prevents fish movement.
        - **:Passable** — "Passable"
          _def:_ An obstruction that does not fully block fish movement.
    - **:WaterFlow** — "Water Flow"
      _def:_ The relative discharge or velocity of stream water at the time of observation.
      - **:HighFlow** — "High Flow"
        _def:_ Stream discharge or velocity that is higher than typical seasonal levels.
      - **:LowFlow** — "Low Flow"
        _def:_ Stream discharge or velocity that is lower than typical seasonal levels.
- **:Impact** — "Impact"
  - **:FishPassageBarrier** — "Fish Passage Barrier"
    _def:_ A condition or structure that impedes or prevents fish movement.
  - **:IncreasedSedimentation** — "Increased Sedimentation"
    _def:_ Elevation in fine sediment delivery or deposition within the channel.
  - **:PredationPressure** — "Predation Pressure"
    _def:_ Elevated risk of mortality or injury to salmon due to predator presence and activity.
  - **:ReducedConnectivity** — "Reduced Connectivity"
    _def:_ Loss or reduction of hydraulic connection among channel segments or habitats.
  - **:SpawningHabitatScour** — "Spawning Habitat Scour"
    _def:_ Removal or disturbance of spawning gravels due to high flows.
- **:Inspection** — "Inspection"
- **:InspectionDetails** — "Inspection Details"
  - **:CountType** — "Count Type"
  - **:DataQualityFlag** — "Data Quality Flag"
  - **:DetectionMethod** — "Detection Method"
  - **:EffortUnit** — "Effort Unit"
  - **:Gear** — "Gear"
  - **:InspectionMethod** — "Inspection Method"
    - **:AerialMethod** — "Aerial Method"
    - **:GroundMethod** — "Ground-based Method"
  - **:MediaObject** — "Media Object"
  - **:Organization** — "Organization"
  - **:Permit** — "Permit"
  - **:Person** — "Person"
  - **:Protocol** — "Protocol"
  - **:Role** — "Role"
- **:Region** — "Region"
  - **:CountryOrState** — "Country or State/Province"
  - **:Estuary** — "Estuary"
  - **:LandRegion** — "Land Region"
  - **:OceanBasin** — "Ocean Basin"
- **:Salmon** — "Salmon Characteristics"
  - **:BiologicalActivity** — "Biological Activities"
    _def:_ Observed level of salmon biological activity (e.g., feeding, holding, spawning) during inspection.
    - **:EnhancedActivity** — "Enhanced Activity"
      _def:_ Activity levels above typical expectations for the site and season.
    - **:IntenseActivity** — "Intense Activity"
      _def:_ Markedly elevated activity characterized by conspicuous behaviors (e.g., active spawning, aggressive interactions).
  - **:Jack** — "Jack"
    _def:_ A precociously maturing male salmon that returns to spawn at a younger age and smaller size than typical adults.
  - **:Juvenile** — "Juvenile"
    _def:_ A young salmon prior to reaching sexual maturity.
  - **:PredatorObservation** — "Predators"
    _def:_ Observation of predators interacting with or near salmon.
    - **:BearPredator** — "Bear"
      _def:_ Observation of bears preying upon or scavenging salmon.
    - **:SealPredator** — "Seal"
      _def:_ Observation of seals preying upon salmon, typically in estuarine or nearshore reaches.
  - **:Redd** — "Redd"
    _def:_ A nest excavated by a female salmon in gravel substrate for depositing eggs.
  - **:SalmonSpecies** — "Salmon Species"
    _def:_ Taxonomic species of salmon observed during inspections.
  - **:SpawningHabitatDegradation** — "Spawning Habitat Degradation"
    _def:_ A decline in the quality of gravel spawning habitat due to factors such as fine sediment, scouring, or pollution.
  - **:UnusualMortality** — "Unusual Mortalities"
    _def:_ Elevated or atypical mortality of salmon beyond expected baseline for the season or site.
  - **:VariationInSexRatio** — "Variation in Sex Ratio"
    _def:_ An observed deviation from the expected proportion of males to females in a salmon group.
- **:WaterbodyIdentifier** — "Waterbody Identifier"