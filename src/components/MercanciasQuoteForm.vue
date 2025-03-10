<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold text-gray-800 mb-4">Cotización Mercancías por Trayecto</h1>
    <div class="grid grid-cols-2 gap-4">
      <!-- Datos del Cliente -->
      <div class="bg-blue-100 p-4 rounded-md shadow-sm">
        <h2 class="text-lg font-semibold mb-2 text-gray-700">
          Datos del Cliente
        </h2>
        <div class="grid grid-cols-1 gap-2">
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">RUT Cliente</label>
            <input type="text" v-model="formData.rutCliente" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Nombre del Cliente</label>
            <input type="text" v-model="formData.nombreCliente" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Email del Cliente</label>
            <input type="email" v-model="formData.emailCliente" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Teléfono del Cliente</label>
            <input type="tel" v-model="formData.telefonoCliente" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Empresa GPS</label>
            <select v-model="formData.empresaGPS" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
              <option value="">Seleccione empresa GPS</option>
              <option v-for="empresa in empresasGPS" :key="empresa" :value="empresa">{{ empresa }}</option>
            </select>
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Dirección del Cliente</label>
            <input type="text" v-model="formData.direccionCliente" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Código Postal</label>
            <input type="text" v-model="formData.codigoPostal" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Región</label>
            <select v-model="formData.region" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
              <option value="">Seleccione una región</option>
              <option v-for="region in regiones" :key="region" :value="region">{{ region }}</option>
            </select>
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Comuna</label>
            <select v-model="formData.comuna" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
              <option value="">Seleccione una comuna</option>
              <option v-for="comuna in comunas" :key="comuna" :value="comuna">{{ comuna }}</option>
            </select>
          </div>
        </div>
      </div>

      <!-- Datos del Viaje -->
      <div class="bg-blue-100 p-4 rounded-md shadow-sm">
        <h2 class="text-lg font-semibold mb-2 text-gray-700">
          Datos del Viaje
        </h2>
        <div class="grid grid-cols-1 gap-2">
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Tipo de Mercancía</label>
            <select v-model="formData.tipoMercancia" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
              <option value="">Seleccione tipo de mercancía</option>
              <option v-for="tipo in tiposMercancia" :key="tipo" :value="tipo">{{ tipo }}</option>
            </select>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Límite de Indemnización</label>
              <input type="number" v-model="formData.limiteIndemnizacion" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Precio</label>
              <input type="number" v-model="formData.precio" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Región de Origen</label>
              <select v-model="formData.regionOrigen" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione una región</option>
                <option v-for="region in regiones" :key="region" :value="region">{{ region }}</option>
              </select>
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Comuna de Origen</label>
              <select v-model="formData.comunaOrigen" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione una comuna</option>
                <option v-for="comuna in comunas" :key="comuna" :value="comuna">{{ comuna }}</option>
              </select>
            </div>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Región Destino Final</label>
              <select v-model="formData.regionDestino" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione una región</option>
                <option v-for="region in regiones" :key="region" :value="region">{{ region }}</option>
              </select>
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Comuna Destino Final</label>
              <select v-model="formData.comunaDestino" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione una comuna</option>
                <option v-for="comuna in comunas" :key="comuna" :value="comuna">{{ comuna }}</option>
              </select>
            </div>
          </div>
          <div class="grid grid-cols-4 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Paradas</label>
              <select v-model="formData.tieneParadas" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione</option>
                <option value="Si">Sí</option>
                <option value="No">No</option>
              </select>
            </div>
            <div v-if="formData.tieneParadas === 'Si'">
              <label class="block text-gray-700 text-sm font-bold mb-2">Parada 1</label>
              <input type="text" v-model="formData.parada1" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div v-if="formData.tieneParadas === 'Si'">
              <label class="block text-gray-700 text-sm font-bold mb-2">Parada 2</label>
              <input type="text" v-model="formData.parada2" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div v-if="formData.tieneParadas === 'Si'">
              <label class="block text-gray-700 text-sm font-bold mb-2">Parada 3</label>
              <input type="text" v-model="formData.parada3" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Fecha de Inicio del Viaje</label>
              <input type="date" v-model="formData.fechaInicio" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Hora de Inicio del Viaje</label>
              <input type="time" v-model="formData.horaInicio" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Fecha de Fin del Viaje</label>
              <input type="date" v-model="formData.fechaFin" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Hora de Fin del Viaje</label>
              <input type="time" v-model="formData.horaFin" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div class="grid grid-cols-2 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Guía de Despacho / Factura</label>
              <input type="text" v-model="formData.guiaDespacho" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Adjuntar documento</label>
              <input type="file" @change="handleFileUpload" class="shadow appearance-none border rounded w-full py-1.5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div class="grid grid-cols-3 gap-2">
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Patente Camión / Tracto-Camión</label>
              <input type="text" v-model="formData.patenteCamion" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Remolque / Semi-Remolque</label>
              <select v-model="formData.tieneRemolque" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm">
                <option value="">Seleccione</option>
                <option value="Si">Sí</option>
                <option value="No">No</option>
              </select>
            </div>
            <div>
              <label class="block text-gray-700 text-sm font-bold mb-2">Patente Remolque / Semi-Remolque</label>
              <input type="text" v-model="formData.patenteRemolque" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
            </div>
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Nombre del Conductor</label>
            <input type="text" v-model="formData.nombreConductor" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Teléfono del Conductor</label>
            <input type="tel" v-model="formData.telefonoConductor" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2">Email del Conductor</label>
            <input type="email" v-model="formData.emailConductor" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline text-sm" />
          </div>
        </div>
      </div>
    </div>

    <!-- Cálculo Prima Final -->
    <div v-if="showPrima" class="mt-6 bg-white p-4 rounded-lg shadow-md">
      <h2 class="text-lg font-semibold mb-4 text-gray-800">Cálculo Prima Final</h2>
      <table class="min-w-full bg-white border border-gray-300 rounded-lg overflow-hidden">
        <thead class="bg-gray-100">
          <tr>
            <th class="px-6 py-3 text-left text-sm font-semibold text-gray-700">Concepto</th>
            <th class="px-6 py-3 text-right text-sm font-semibold text-gray-700">Valor (UF)</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-300">
          <tr>
            <td class="px-6 py-4 text-sm text-gray-700">Prima Neta</td>
            <td class="px-6 py-4 text-right text-sm font-medium">{{ primaNeta }}</td>
          </tr>
          <tr>
            <td class="px-6 py-4 text-sm text-gray-700">IVA</td>
            <td class="px-6 py-4 text-right text-sm font-medium">{{ iva }}</td>
          </tr>
          <tr class="bg-blue-50">
            <td class="px-6 py-4 text-sm font-bold text-gray-800">Prima Total</td>
            <td class="px-6 py-4 text-right text-lg font-bold text-blue-700">{{ primaTotal }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Botón Calcular -->
    <div class="flex justify-center mt-6">
      <button @click="calcularPrima" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded-lg focus:outline-none focus:shadow-outline">
        Cálculo Prima Final
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

const showPrima = ref(false);
const primaNeta = ref(1.75);
const iva = ref(0.34);
const primaTotal = ref(2.09);

const empresasGPS = [
  "2REALP", "4GPS", "4TRACK", "ADS LOGIC", "ADVANTANGE - MALFAVON - UTS", "ALL TRACK",
  "TRACK SOLID", "ARGOS", "ARVOS", "ASTUS", "ATLANTIDA", "AUTOFLETES CHIHUAHUA",
  "AUTOLINEAS AMERICA - ALIANZA TRAYECTO", "AVANTEC", "AVILSAT", "AVITEC",
  "BASHO  - POSITION LOGIC", "BLAC SOLUTIONS - POSITION LOGIC", "BLACK POINT",
  "BLOOMOTION", "BOSONTI", "BRANIX", "CASTORES", "CEBALLOS", "CIRCULO CORP",
  "COBRA", "COMDATA", "CONTROL TRACK - POSITION LOGIC", "COPILOTO - SMART",
  "COSO AVL", "CSI TRACK", "CTRACK", "CTS CONTROL", "CYBERMAPA", "CYRUS",
  "DECAWEB - GRUPO DECA", "DELTAGPS", "DETECTOR", "DIGITOOLS", "DUMAX", "DVTRACE",
  "EASY TRACK", "EGOBA", "EMOVIL", "EMSAT", "ENCONTRACK", "ENERGIA 40", "EPCOM",
  "ESGARI", "EVERTRACK", "EZTRACK", "FEMA", "FLEETTRACKERS", "FLOTIMATICS",
  "FRIO EXPRESS", "FULLTRACK  - GPSFULLTIME - PROCOMMEX - VICUSA", "GCCOMERCE",
  "GECKOTECH", "GEOTAB - METRICA MOVIL", "GLOBAL MIT", "GLOBAL TRACK", "GM TRANSPORT",
  "GOSMO", "GPOBSI - UBICAWARE", "GPS TECHTRACK", "GPS TECNOLOGIAS", "GPS TOTAL",
  "GPS-i PROTECTED", "GPS MOVIL", "GPS TrackerXY", "GRUPO SILSA", "GUARD EAGLE",
  "HOLKAN", "ICOGLO", "ILSP", "INGENIERIATIC", "INNOVALINKS", "INTERNACIONAL  GPS",
  "INTRALIX", "KOMETSATELITAL", "KOSMOS POSITION LOGIC", "KOSMOS - UTRAX", "LANSAT",
  "LARMEX", "LO JACK", "LOCALIZADORES GTS - GLOBAL TRACKING SYSTEM", "LOCASAT",
  "LOCATEK - SIS TECNOLOGIAS", "LOGICTRACKER", "LOGISTIC GPS", "LOGITRACK", "LOGSYS",
  "LU3O", "MASTERTRACK", "MASTRACK CSI - FLEETCOMPLETE", "MAYAN", "MEERKAT SYSTEMS",
  "MEXTIC", "MEXTRACKER", "MGSATELITAL", "MI TRACK - VELTRACK", "MILENIUMTRACK",
  "MONITOREO Y RASTREO - PROTECTED", "MOTUM", "MOTUMWEB", "MULTIALARMAS",
  "MULTIMODAL MEXICANO - TIMSA", "MULTITRACK", "NAVICGATION", "NAVMAN", "NORTTREK",
  "NUVE", "OMNICEL", "OMNITRACS", "ONTRACKING", "OPTIMUS GPS", "ORIGIN GPS",
  "PICUS - OMNITRACS", "P-LOCK", "POINTER", "POSITION LOGIC - VALE SATELICAL",
  "POSITIONS PLUS", "POSITRACE", "PROCOMMEX - GPSFULLTIME - FULLTRACK", "PROTECTED",
  "PSLOG", "RACS SEGURIDAD", "RAINDE", "RASTREO", "REC SOLUTIONS", "REGIOTRANSPORTES",
  "RELECTRONIC", "RESSER", "SASCAR", "SECURITE TELEMATICA - CTTMX", "SEEKERS", "SEND",
  "SEPROMEX", "SERIOUS", "SERVINGENIERIA", "SGLOCALIZACION", "SGIT", "SICSA", "SIETE",
  "SITRACK", "SKY ANGEL - POSITION LOGIC", "SKY GUARDIAN", "SKY MEDUZA", "SKY WORLD",
  "SLTRACKER", "SMARTTRACKER", "SOLTRACK", "SOLUSOF", "SOS SOLUTRANS", "SOSGPS",
  "SUPERTRACK", "SUVI", "SYSTEI", "TAO", "TCVSAT", "TECNOLOGIASIS",
  "TECNOLOGISTIK - POSITION LOGIC", "TELCEL", "TELCELCIRCULOCORP", "TELEMATICS",
  "TELEMETRY", "TILATINA", "TI-MOBILE", "TIUSA", "TMS", "TRAAK", "TRABAL",
  "TRACK JACK - NEXTRACK", "TRACK NAVIGATION", "TRACK ONE", "TRACKERMEX",
  "TRACKING CENTER - GPS TTC", "TRACKINGCO", "TRACKLOCATOR", "TRAFFILOG", "TRANCASA",
  "TRANSMONTES", "TRANSPLACE", "TRANSPORTES MONTERREY", "TRONCAL NET", "TRUCKA", "TUM",
  "TUMSA", "UBIC", "UBICALO", "UBICAWARE", "UBIKNOS", "UBIQO", "UDA - OVISION",
  "USAMEX", "VECTIUM", "VECTRO", "VERSO CONTROLS", "WIALON", "WIDETECH", "WORLDFLEETLOG",
  "YETCARGO", "ZEEK GPS", "EQUS GPS", "GLOBAL SAT", "GPS TOTAL", "GTS GLOBAL",
  "HOME LINUX", "INFO TRAX", "INOVAMETRICA", "ISCA", "KANAAN - POSITION LOGIC",
  "LOCANET", "LOCMEX", "MEXTIC", "NEXTRACK", "REDINMEX", "SILSA", "SINTEL", "SITS",
  "SMC - SOLUCIONES MOVILES", "TRACKING UDA", "VALE SATELITAL", "VICUSA", "APS MOVILES",
  "ONROUTE", "BROVE", "TECNOCONTROL", "GFHK PROMOTORES", "LOGISTICARE", "COPA SEGUROS",
  "SERVISEG"
];

const tiposMercancia = [
  'Agroquímicos',
  'Artículos de Bazar y Regalería',
  'Artículos de Ferretería',
  'Artículos de Iluminación',
  'Artículos de Librería',
  'Artículos de Perfumería',
  'Artículos deportivos',
  'Artículos Fotográficos',
  'Autoelevadores',
  'Baldosas, Cerámicos y/o Azulejos',
  'Bebidas Alcoholicas',
  'Bebidas No Alcoholicas',
  'Bicicletas',
  'Calzado en General',
  'CañOs y/o Tubos De Hierro Y/O Acero',
  'CañOs y/o Tubos De Plastico',
  'Cargador Frontal',
  'Chapa De Hierro y/o Acero',
  'Combustibles y/o Lubricantes',
  'Comestibles',
  'Confecciones Textiles en General',
  'Cosméticos',
  'Electrodomésticos',
  'Equipos de Laboratorio',
  'Equipos e Insumos Petroleros',
  'Fertilizantes',
  'Grifería',
  'Herramientas de Mano',
  'Hilados',
  'Hojalata',
  'Libros, Revistas',
  'Máquinas Agrícolas',
  'Máquinas de Imprenta',
  'Máquinas Industriales',
  'Máquinas Textiles',
  'Máquinas Viales',
  'Materia Prima Farmacéutica',
  'Materia Prima para Ind. Plástica',
  'Metales En Lingotes y/o Barras y/o Barillas',
  'Motocicletas',
  'Papel en Bobinas',
  'Papel en Resmas',
  'Pinturas, Pigmentos Y Similares',
  'Productos Químicos',
  'Sanitarios',
  'Telas / Hilados'
];

const regiones = [
  'Arica y Parinacota',
  'Tarapacá',
  'Antofagasta',
  'Atacama',
  'Coquimbo',
  'Valparaíso',
  'Metropolitana',
  'O\'Higgins',
  'Maule',
  'Ñuble',
  'Biobío',
  'La Araucanía',
  'Los Ríos',
  'Los Lagos',
  'Aysén',
  'Magallanes'
];

const comunas = [
  'Santiago',
  'Providencia',
  'Las Condes',
  'Ñuñoa',
  'La Florida',
  'Maipú',
  'Puente Alto',
  'Vitacura',
  'Lo Barnechea',
  'La Reina'
];

const formData = reactive({
  rutCliente: '',
  nombreCliente: '',
  emailCliente: '',
  telefonoCliente: '',
  empresaGPS: '',
  direccionCliente: '',
  codigoPostal: '',
  region: '',
  comuna: '',
  tipoMercancia: '',
  limiteIndemnizacion: '',
  precio: '',
  regionOrigen: '',
  comunaOrigen: '',
  regionDestino: '',
  comunaDestino: '',
  tieneParadas: '',
  parada1: '',
  parada2: '',
  parada3: '',
  fechaInicio: '',
  horaInicio: '',
  fechaFin: '',
  horaFin: '',
  guiaDespacho: '',
  patenteCamion: '',
  tieneRemolque: '',
  patenteRemolque: '',
  nombreConductor: '',
  telefonoConductor: '',
  emailConductor: ''
});

const handleFileUpload = (event) => {
  const file = event.target.files[0];
  // Handle file upload logic here
  console.log('File selected:', file);
};

const calcularPrima = () => {
  showPrima.value = true;
};
</script>