# test-repo-ever

import { publish, MessageContext } from 'lightning/messageService';
import { NavigationMixin } from 'lightning/navigation';
import { LightningElement, wire, api } from 'lwc';
import { getRecord, getFieldValue } from 'lightning/uiRecordApi';
const TILE_WRAPPER_SELECTED_CLASS="tile-wrapperselected";
const TILE_WRAPPER_UNSELECTED_CLASS= "tile-wrapper";
// imports
export default class BoatTile extends LightningElement {
   @api boat;
   @api selectedBoatId;
   
    // Getter for dynamically setting the background image for the picture
    get backgroundStyle() {
      return `background-image:url(${this.boat.Picture__c})`;
     }
    
    // Getter for dynamically setting the tile class based on whether the
    // current boat is selected
    get tileClass() { 
      return (this.selectedBoatId==this.boat.Id )? TILE_WRAPPER_SELECTED_CLASS : TILE_WRAPPER_UNSELECTED_CLASS;
      }
    
    
    // Fires event with the Id of the boat that has been selected.
    selectBoat() { 

      const boatId = this.boat.Id;
      const boatSearchResults  = new CustomEvent('boatselect', { detail: this.boatId });
      publish(this.messageContext, BOATMC, boatSearchResults);
    }
  }