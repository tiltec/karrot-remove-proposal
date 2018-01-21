<template>
  <div style="max-width: 800px">
    <h4>
      Removal process demo (Brainstorming)
    </h4>
    <q-alert
      color="red"
      icon="warning"
    >
      Bob requested to remove X from the group. Please read through the conversation and give your opinion afterwards. The vote will run until at least half of all group members have voted, plus three days. The result will be shown after the vote ended. As long as the vote is ongoing, you can change your opinion anytime.
    </q-alert>
    <q-list>
      <q-item>
        65% of fellow group members voted already. Remaining time: 1 day 10 hours
      </q-item>
      <q-item>
        <q-progress
          :percentage="65"
          color="green"
          style="height: 12px"
        />
      </q-item>
    </q-list>
    <q-card>
      <q-card-title>
        Conversation
      </q-card-title>
      <q-card-main>
        <q-chat-message
          v-for="msg in messages"
          :key="msg"
          avatar="statics/quasar-logo.png"
          :label="msg.label"
          :name="msg.name"
          :text="msg.text"
          :sent="msg.sent"
          :bg-color="msg.bg"
        />
        <q-field>
          <q-input placeholder="You can comment here..." />
        </q-field>
      </q-card-main>
    </q-card>
    <q-card>
      <q-card-title>
        Do you have enough information to make a decision?
      </q-card-title>
      <q-card-main>
        <q-option-group
          type="radio"
          v-model="repeat"
          :options="repeatOptions"
        />
        <small class="text-italic">(Options are shuffled on page load)</small>
      </q-card-main>
      <q-card-separator />
      <q-card-main>
        In case you don't have enough information, you can still give your opinion.
      </q-card-main>
    </q-card>
    <q-card>
      <q-card-title>
        Should user X be removed from group "ASDF"?
      </q-card-title>
      <q-card-main>
        <q-option-group
          type="radio"
          v-model="kick"
          :options="kickOptions"
        />
        <small class="text-italic">(Options are shuffled on page load)</small>
      </q-card-main>
    </q-card>
    <q-card>
      <q-card-title>
        Submit
      </q-card-title>
      <q-card-main>
        <q-btn color="primary">Save vote</q-btn>
      </q-card-main>
    </q-card>
    <h4>
      Demo of result pages
    </h4>
    <q-card>
      <q-card-title>
        Results <small>(undecided but time expired)</small>
      </q-card-title>
      <q-card-main>
        <p>Most people said that they don't have enough information regarding this decision, therefore the voting period is extended until more people are certain.</p>
        <q-list>
          <q-item class="group">
            <span style="width: 6em">Not enough information</span>
            <q-progress color="yellow" :percentage="78" style="height: 12px" />
            78%
          </q-item>
          <q-item-separator />
          <q-item class="group">
            <span style="width: 6em">No</span>
            <q-progress :percentage="0" style="height: 12px" />
            ?&nbsp;%
          </q-item>
          <q-item class="group">
            <span style="width: 6em">Yes</span>
            <q-progress :percentage="0" style="height: 12px" />
            ?&nbsp;%
          </q-item>
          <q-item class="group">
            <span style="width: 6em">I don't care</span>
            <q-progress :percentage="0" style="height: 12px" />
            ?&nbsp;%
          </q-item>
        </q-list>
      </q-card-main>
    </q-card>
    <q-card>
      <q-card-title>
        Results <small>(decided)</small>
      </q-card-title>
      <q-card-main>
        <p>The process has ended and the result is that most people would rather leave X in the group than remove X.</p>
        <q-list>
          <q-item class="group">
            <span style="width: 6em">No</span>
            <q-progress :percentage="64" style="height: 12px" />
            64%
          </q-item>
          <q-item class="group">
            <span style="width: 6em">Yes</span>
            <q-progress :percentage="34" style="height: 12px" />
            34%
          </q-item>
          <q-item class="group">
            <span style="width: 6em">I don't care</span>
            <q-progress :percentage="12" style="height: 12px" />
            12%
          </q-item>
          <q-item-separator />
          <q-item class="group">
            <span style="width: 6em">Not enough information</span>
            <q-progress color="yellow" :percentage="20" style="height: 12px" />
            20%
          </q-item>
        </q-list>
      </q-card-main>
    </q-card>
  </div>
</template>

<script>

function shuffleArray (array) {
  for (var i = array.length - 1; i > 0; i--) {
    var j = Math.floor(Math.random() * (i + 1))
    var temp = array[i]
    array[i] = array[j]
    array[j] = temp
  }
  return array
}

export default {
  data () {
    return {
      kick: null,
      kickOptions: shuffleArray([
        { label: 'I don\'t care', value: 'op3' },
        { label: 'Yes', value: 'op1' },
        { label: 'No', value: 'op2' }
      ]),
      repeat: null,
      repeatOptions: shuffleArray([
        { label: 'Yes', value: 'op1' },
        { label: 'No', value: 'op2' }
      ]),
      messages: [
        {
          name: 'Bob',
          text: ['I think we should remove X from our foodsaving group. He arrived late at the last 3 pickups, did not apologize and made the store dirty.'],
          sent: true
        },
        {
          name: 'X',
          text: ['Are you crazy? You waited at the wrong location every time, blamed me for being late when I finally found you. The boxes in the store fell down because you stacked them in a wrong way, so I couldn\'t carry them properly.']
        },
        {
          name: 'Bob',
          text: ['You\'re telling lies over lies....'],
          sent: true
        },
        {
          label: 'Decision process was started, all group members added to the conversation',
          name: 'Other member',
          bg: 'yellow',
          text: ['Where did it happen?', 'The meeting place for pickup xyz is quite hard to find...']
        },
        {
          name: 'One more member',
          bg: 'orange',
          text: ['I had both problems with Bob and X so far, but I think both are valuable foodsavers and you should continue saving food. Maybe you just don\'t go to pickups together?']
        }
      ]
    }
  }
}
</script>

<style lang="stylus">
@import '~variables'
</style>
